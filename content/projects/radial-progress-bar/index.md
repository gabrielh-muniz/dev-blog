---
title: Radial Progress Bar
date: "2024-09-02"
draft: false
cover:
    image: img/cover.jpg
    alt: "Image of a purple radial progress bar with a percent indicator in the center"
summary: "This project involves creating a dynamic progress bar using HTML, CSS, and JavaScript."
tags: ["HTML", "CSS", "JS"]
---

## Links

* [setInterval()](https://developer.mozilla.org/en-US/docs/Web/API/setInterval)

## Description

This project is a dynamic progress bar implemented using HTML, CSS and JavaScript. The goal of this project is to train how to schedule an execution. For this project I use a function call `setInterval`. It allows us to run a function repeatedly.

## Source Code

### HTML
{{< highlight html >}}
<div class="progress-bar">
  <span class="progress-value">0</span>
</div>
{{< / highlight >}}

### CSS
{{< highlight css >}}
*, *::before, *::after {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}

.progress-bar {
  position: relative;
  width: 245px;
  height: 245px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
  background: conic-gradient(#7d2ae8 0deg, #ededed 0deg);
}

.progress-bar::before {
  content: "";
  position: absolute;
  width: 225px;
  height: 225px;
  border-radius: 50%;
  background-color: #fff;
}

.progress-value {
  position: relative;
  font-size: 3rem;
  font-family: monospace;
}
{{< / highlight >}}

### JavaScript

{{< highlight js >}}
const progress = document.querySelector('.progress-bar')
const progressValue = document.querySelector('.progress-value')

const progressLength = 100
let progressCount = 0
let dist = 0

let intervalId = setInterval(() => {
  progressCount++
  
  progressValue.innerText = `${progressCount}%`
  
  progress.style.background = `conic-gradient(#7d2ae8 ${progressCount * 3.6}deg, #ededed 0deg)`
  
  if (progressCount == progressLength) {
    progressCount = 0
  }
}, 50)
{{< / highlight >}}
