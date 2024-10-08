---
title: Guess the Number Game
date: "2024-09-03"
draft: false
cover:
    image: img/cover.png
    alt: "Image containing the card game"
summary: "A simple web-based game where the player tries to guess a randomly generated number within a specified range."
tags: ["HTML", "CSS", "JS"]
---

## Description

**Guess the Number** is a fun game where players try to guess a hidde number generated by the computer. The goal is to guess the corret number within a specified range (e.g., 1 to 10) in as few attempts as possible. With each guess, the game provides feedback indicating the number of tries and a list of tried numbers. It's great for a beginner project to practice HTML, CSS and JavaScript.

## How to play

1. The game randomly selects a number within a given range (e.g., 1 to 10).
2. Enter your guess int the input box.
3. Click the "Guess" button to submit your guess.
4. The game will provide feedback:
    - Increment the number of tries and append the guessed number to a list if your guess is not correct.
    - Otherwise, it will be prompt a win message and will restart the game automatically after 3 seconds.

## Project Structure

```bash
guess-number/
├── index.html
├── style.css
└── script.js
```

## Source Code 

### HTML
{{< highlight html >}}
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Guess the Number</title>
  <link href="style.css" rel="stylesheet">
</head>

<body>
  <div class="container">
    <div class="title">
      <h1>Guess the number!</h1>
      <p>I'm thinking of a number between 1-10</p>
      <p>Can you guess it?</p>
    </div>
    <div class="input-wrapper">
      <input type="text" id="guess" />
      <input type="button" value="Guess" class="guess-btn" />
    </div>
    <div class="answer-wrapper">
      <p>No. of guesses: <span class="n-guesses">0</span></p>
      <p>Guessed numbers: <span class="guessed-list">None</span></p>
    </div>
    <div class="result-wrapper">
      <p class="p-result">Correct! The game will restart in <span class="timer">3</span>s</p>
    </div>
  </div>
  <script src="script.js"></script>
</body>

</html>
{{< / highlight >}}

### CSS
{{< highlight css >}}
@import url('https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap');

*,
*:before,
*:after {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html,
body {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-color: #033e97;
  font-family: "Poppins", sans-serif;
}

.container,
.title,
.input-wrapper,
.answer-wrapper,
.result-wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  flex-wrap: wrap;
}

.container {
  gap: 1.3em;
  width: 100%;
  max-width: 31.25em;
  padding: 2em;
  box-shadow: 0.4em 0.4em #202020;
  background-color: #fff;
}

.title h1 {
  font-size: 1.5em;
  margin-bottom: 0.3em;
}

.title>p {
  font-size: 1em;
}

.input-wrapper {
  gap: 1.2em;
}

.input-wrapper #guess {
  width: 70px;
  height: 70px;
  border: 2px solid #202020;
  border-radius: 50%;
  text-align: center;
  font-size: 1.3em;
  outline: none;
  transition: all .2s ease;
}

#guess:focus {
  border-color: #3c6fff;
}

.input-wrapper .guess-btn {
  width: 100px;
  padding: .6em 0;
  border: none;
  border-radius: .5em;
  background-color: #663399;
  color: #fff;
  outline: none;
  cursor: pointer;
  transition: all .2s ease;
}

.guess-btn:hover {
  background-color: #3c6fff;
}

.answer-wrapper p {
  word-break: break-all;
}

.result-wrapper {
  justify-content: center;
  width: 100%;
  height: 35px;
}

.result-wrapper .p-result {
  font-size: 0.8em;
  display: none;
}

.success {
  padding: 0 .4em;
  background-color: #b9ffd5;
  animation: pop .4s forwards;
}

@keyframes pop {
  0% {
    transform: scale(0);
  }

  100% {
    transform: scale(1);
  }
}

@keyframes horizontal-shake {
  0% {
    transform: translateX(0)
  }

  25% {
    transform: translateX(5px)
  }

  50% {
    transform: translateX(-5px)
  }

  75% {
    transform: translateX(5px)
  }

  100% {
    transform: translateX(0)
  }
}

.animate {
  animation: horizontal-shake 0.25s ease-in-out;
}
{{< / highlight >}}

### JavaScript

{{< highlight js >}}
const userGuess = document.querySelector('#guess');
const btn = document.querySelector('.guess-btn');
const par = document.querySelector('.p-result');
const timer = document.querySelector('.timer');
const numberOfGuesses = document.querySelector('.n-guesses');
const guessed = document.querySelector('.guessed-list');

function randomNumber() {
  return Math.floor(Math.random() * 10) + 1;
}

function clearFormatting(array) {
  array.forEach((element) => {
    element.textContent = '';
  });
}

let number = randomNumber();
let countdownTime = 3;
let counterGuesses = 0
clearFormatting([guessed]);

btn.addEventListener('click', (ev) => {
  ev.preventDefault();

  userInput = userGuess.value;
  if (userInput != number) {
    userGuess.classList.add('animate');
    counterGuesses++;
    numberOfGuesses.textContent = counterGuesses;
    guessed.textContent += `${userInput}, `;
    userGuess.value = '';

  } else {
    par.style.display = 'block';
    par.classList.add('success');

    const countdownInterval = setInterval(() => {
      countdownTime--;
      timer.textContent = countdownTime;

      if (countdownTime <= 0) {
        clearInterval(countdownInterval);
        par.style.display = 'none';
        number = randomNumber();
        countdownTime = 3;
        timer.textContent = countdownTime;
        numberOfGuesses.textContent = '0';

        clearFormatting([userGuess, guessed]);

        par.addEventListener('animationend', () => {
          par.classList.remove('success');
        });
      }
    }, 1000);
  }
  userGuess.addEventListener('animationend', () => {
    userGuess.classList.remove('animate');
  });
});
{{< / highlight >}}

