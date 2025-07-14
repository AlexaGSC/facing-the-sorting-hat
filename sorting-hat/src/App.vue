<template>
  <main class="chat-container">
    <div class="messages">
      <div
        v-for="(msg, index) in messages"
        :key="index"
        :class="['message', msg.sender]"
      >
        <p>{{ msg.text }}</p>
      </div>
    </div>

    <div class="input-area" v-if="awaitingInput">
      <input
        v-model="userInput"
        @keyup.enter="handleInput"
        placeholder="Type your answer..."
      />
      <button @click="handleInput">Send</button>
    </div>
  </main>
</template>

<script setup>
import { ref, reactive, onMounted } from 'vue'
import questions from './data/questions.json'

const messages = ref([])
const currentQuestionIndex = ref(0)
const userName = ref('')
const awaitingInput = ref(true)
const userInput = ref('')

const scores = reactive({
  G: 0,
  H: 0,
  R: 0,
  S: 0
})

onMounted(() => {
  messages.value.push({
    sender: 'bot',
    text: '🧙‍♂️ Welcome, young wizard! What is your name?'
  })
})

function handleInput() {
  const input = userInput.value.trim()
  if (!input) return

  messages.value.push({
    sender: 'user',
    text: input
  })

  userInput.value = ''
  awaitingInput.value = false

  if (!userName.value) {
    userName.value = input
    nextQuestion()
  } else {
    const question = questions[currentQuestionIndex.value]
    const selectedAnswer = question.answers.find(a =>
      a.title.toLowerCase() === input.toLowerCase()
    )

    if (!selectedAnswer) {
      messages.value.push({
        sender: 'bot',
        text: 'Please type one of the exact answers shown above.'
      })
      awaitingInput.value = true
      return
    }

    for (const [house, points] of Object.entries(selectedAnswer.scores)) {
      scores[house] += points
    }

    currentQuestionIndex.value++
    nextQuestion()
  }
}

function nextQuestion() {
  if (currentQuestionIndex.value >= questions.length) {
    const highestHouse = Object.entries(scores).sort((a, b) => b[1] - a[1])[0][0]

    const houseNames = {
      G: '🦁 Gryffindor',
      H: '🦡 Hufflepuff',
      R: '🦅 Ravenclaw',
      S: '🐍 Slytherin'
    }

    messages.value.push({
      sender: 'bot',
      text: `🎉 ${userName.value}, you belong to ${houseNames[highestHouse]}!`
    })
    return
  }

  const question = questions[currentQuestionIndex.value]

  messages.value.push({
    sender: 'bot',
    text: `❓ ${question.title}`
  })

  question.answers.forEach(answer => {
    messages.value.push({
      sender: 'bot',
      text: `👉 ${answer.title}`
    })
  })

  awaitingInput.value = true
}
</script>

<style scoped>
.chat-container {
  max-width: 600px;
  margin: 2rem auto;
  padding: 1rem;
  background: #c9c8c8;
  border-radius: 12px;
  font-family: 'Segoe UI', sans-serif;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

.messages {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  max-height: 70vh;
  overflow-y: auto;
  padding-bottom: 1rem;
}

.message {
  padding: 0.75rem 1rem;
  border-radius: 10px;
  max-width: 80%;
  line-height: 1.4;
}

.message.bot {
  background-color: #5a5a5a;
  align-self: flex-start;
}

.message.user {
  background-color: #225386;
  align-self: flex-end;
}

.input-area {
  display: flex;
  gap: 0.5rem;
  margin-top: 1rem;
}

input {
  flex: 1;
  padding: 0.75rem;
  border-radius: 8px;
  border: 1px solid #ccc;
}

button {
  padding: 0.75rem 1rem;
  border-radius: 8px;
  border: none;
  background-color: #1f4979;
  color: white;
  cursor: pointer;
  transition: background-color 0.2s ease-in-out;
}

button:hover {
  background-color: #357abd;
}
</style>
