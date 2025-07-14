# 🧙‍♂️ Sorting Hat Chat App

An animated, chat-based Vue.js application that assigns users to one of the four Hogwarts houses based on their responses to a personality test.

This project was created as a front-end technical assessment using **Vue 3 + Vite**, with a strong focus on **UX**, **maintainability**, and **animation**.

---

## 🎯 Features

- 💬 **Chat-based UI** for a conversational test experience
- 🧠 **Dynamic scoring** system that attributes points to houses based on answers
- 🔄 **Smooth animations** when sending and receiving messages
- 🎨 **Responsive layout**, optimized from mobile to desktop
- 🔧 Built using **Composition API**, **Vite**, and clean component-based architecture

---

## 🧰 Tech Stack

- [Vue 3](https://vuejs.org/)
- [Vite](https://vitejs.dev/)
- CSS (Scoped)

## 📁 Project Structure

sorting-hat/
├── public/
│ └── vite.svg
├── src/
│ ├── data/
│ │ └── questions.json
│ ├── App.vue
│ ├── main.js
│ └── style.css
├── .gitignore
├── index.html
├── package.json
├── package-lock.json
├── README.md
└── vite.config.js

---

## 🧪 Questions & Scoring

The test is structured around multiple-choice questions (MCQs), with each answer contributing specific points to the four Hogwarts houses:

- Gryffindor (G)
- Hufflepuff (H)
- Ravenclaw (R)
- Slytherin (S)

At the end of the test, the house with the **highest score** is shown to the user.

All questions are loaded dynamically from a JSON file: [`questions.json`](./src/data/questions.json)

---

## 🚀 Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/sorting-hat-chat.git
cd sorting-hat-chat

## 🛠️ Install Dependencies

```bash
npm install


## 🚀 Run the App Locally

```bash
npm run dev

Then open http://localhost:5173 in your browser.

## 📦 Build for Production

```bash
npm run build
