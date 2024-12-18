# Ex.08 Design of Interactive Image Gallery
## Date:16/12/2006

## AIM:
To design a web application for an inteactive image gallery with minimum five images.

## DESIGN STEPS:

### Step 1:
Clone the github repository and create Django admin interface.

### Step 2:
Change settings.py file to allow request from all hosts.

### Step 3:
Use CSS for positioning and styling.

### Step 4:
Write JavaScript program for implementing interactivity.

### Step 5:
Validate the HTML and CSS code.

### Step 6:
Publish the website in the given URL.

## PROGRAM :
```
index.html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="style.css">
    <title>Document</title>
</head>
<body>
    <main data-active-index="0" data-debug="false">
        <div class="card-stack">
          <div class="card"><img src="https://assets.codepen.io/215059/card-stack-demo-05.jpg" /></div>
          <div class="card"><img src="https://assets.codepen.io/215059/card-stack-demo-04.jpg" /></div>
          <div class="card"><img src="https://assets.codepen.io/215059/card-stack-demo-06.jpg" /></div>
          <div class="card"><img src="https://assets.codepen.io/215059/card-stack-demo-07.jpg" /></div>
          <div class="card"><img src="https://assets.codepen.io/215059/card-stack-demo-08.jpg" /></div>
        </div>
        <div class="scroller">
          <div class="scroll-item"></div>
          <div class="scroll-item"></div>
          <div class="scroll-item"></div>
          <div class="scroll-item"></div>
          <div class="scroll-item"></div>
        </div>
      </main>
      
      <!-- Everything below this line is for the demo only -->
      <div class="warning">
        <span>Mouse drag not supported. Use responsive mode or a touch pad to scroll.</span>
      </div>
      
      <div class="explainer">
        <input type="checkbox"></input>
        <div>
          <svg id="icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 32 32"><defs><style>.cls-1{fill:none;}</style></defs><title>help</title><path d="M16,2A14,14,0,1,0,30,16,14,14,0,0,0,16,2Zm0,26A12,12,0,1,1,28,16,12,12,0,0,1,16,28Z" fill="white"/><circle cx="16" cy="23.5" r="1.5" fill="white"/><path d="M17,8H15.5A4.49,4.49,0,0,0,11,12.5V13h2v-.5A2.5,2.5,0,0,1,15.5,10H17a2.5,2.5,0,0,1,0,5H15v4.5h2V17a4.5,4.5,0,0,0,0-9Z" fill="white"/></svg>
        </div>
      <p>Inspired by original <a href="https://x.com/nasm423/status/1795133452016054401">Nate Smith</a> demo.</p>
        <p>
          Demo of CSS <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/animation-timeline/scroll#browser_compatibility">scroll()</a> function with <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/scroll-snap-type">scroll-snap</a>, <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/animation-timeline">animation-timeline</a>, and <a href="https://developer.chrome.com/blog/scroll-snap-events">scroll snap events</a>.
        </p>
        <p>
          Requires Chrome 129+. Try in Chrome on Android or in Chrome Desktop responsive mode (use <a href="https://codepen.io/paulnoble/pen/gOVPedz">debug view</a>) or with a trackpad for best scrolling experience.
        </p>
        <p>
       <a href="https://x.com/paul_uiux">paul_uiux@</a></p>
      </div>
      
      <!-- Warn pointer down -->
      <script>
       const warn = () => {
         document.querySelector('.warning').classList.toggle('show');
         setTimeout(() => document.querySelector('.warning').classList.toggle('show'), 3000);
       };
        document.querySelector('main').addEventListener('mousedown', warn);
      </script>
    <script  src="main.js"></script>

</body>
</html>

style.css

@charset "UTF-8";
:root {
  font-family: Inter, system-ui, Avenir, Helvetica, Arial, sans-serif;
  line-height: 1.5;
  font-weight: 400;
  --dim-card-width: 300px;
  --dim-card-height: 400px;
  --dim-card-border-radius: 16px;
  --box-shadow-card: 0 1px 12px rgba(0, 0, 0, 0.4);
}

::-webkit-scrollbar {
  display: none;
}

* {
  box-sizing: border-box;
}

body,
html {
  margin: 0;
  padding: 0;
}

body {
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #ddd;
  height: 100vh;
  min-height: 800px;
  timeline-scope: --scroll-timeline;
  animation: theme-bg linear forwards;
  animation-timeline: --scroll-timeline;
}

main {
  width: 800px;
  height: 600px;
  perspective: 1000px;
  transform-style: preserve-3d;
}

.scroller {
  width: 100%;
  height: 100%;
  overflow: auto;
  white-space: nowrap;
  display: flex;
  scroll-snap-type: x mandatory;
  scroll-timeline: --scroll-timeline;
  scroll-timeline-axis: x;
}

.scroll-item {
  flex: 0 0 100%;
  height: 100%;
  scroll-snap-align: start;
}

[data-debug=true] .scroll-item {
  outline: 1px dashed magenta;
}

.card-stack {
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  transform-style: preserve-3d;
  pointer-events: none;
}

.card {
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  margin: auto;
  width: var(--dim-card-width);
  height: var(--dim-card-height);
  border-radius: var(--dim-card-border-radius);
  display: flex;
  align-items: center;
  justify-content: center;
  transform-style: preserve-3d;
  overflow: hidden;
  background-color: rgba(255, 255, 255, 0.8);
  box-shadow: var(--box-shadow-card);
}

.card img {
  position: absolute;
  object-fit: cover;
  width: 100%;
  z-index: 1;
  height: 100%;
}

.card::before {
  position: absolute;
  top: -4px;
  bottom: -4px;
  right: -4px;
  left: -4px;
  content: "";
}

.card:nth-child(1) {
  animation: animate1-inactive linear forwards;
  animation-timeline: --scroll-timeline;
}

[data-active-index="0"] .card:nth-child(1) {
  animation: animate1-active linear forwards;
  animation-timeline: --scroll-timeline;
}

.card:nth-child(1) img {
  animation: animate-card-image-1 linear forwards;
  animation-timeline: --scroll-timeline;
}

[data-active-index="0"] .card-stack {
  animation: card-stack-1 linear forwards;
  animation-timeline: --scroll-timeline;
}

.card:nth-child(1)::before {
  animation: card-bg linear forwards;
  animation-timeline: --scroll-timeline;
}

@keyframes animate1-active {
  0% {
    transform: translateX(0) rotateY(0) rotateZ(0) rotateX(0) translateZ(0);
  }
  12.5% {
    transform: translateX(-116%) rotateY(-24deg) rotateZ(0) rotateX(2deg) translateZ(-156px);
  }
  25% {
    transform: translateX(-11%) rotateY(0) rotateZ(-6deg) rotateX(0) translateZ(-160px);
  }
  50% {
    transform: translateX(-19%) rotateY(0) rotateZ(-8deg) rotateX(0) translateZ(-180px);
  }
  75% {
    transform: translateX(-27%) rotateY(0) rotateZ(-10deg) rotateX(0) translateZ(-200px);
  }
  100% {
    transform: translateX(-35%) rotateY(0) rotateZ(-12deg) rotateX(0) translateZ(-220px);
  }
}
@keyframes animate1-inactive {
  0% {
    transform: translateX(0) rotateY(0) rotateZ(0) rotateX(0) translateZ(0);
  }
  25% {
    transform: translateX(-11%) rotateY(0) rotateZ(-6deg) rotateX(0) translateZ(-160px);
  }
  50% {
    transform: translateX(-19%) rotateY(0) rotateZ(-8deg) rotateX(0) translateZ(-180px);
  }
  75% {
    transform: translateX(-27%) rotateY(0) rotateZ(-10deg) rotateX(0) translateZ(-200px);
  }
  100% {
    transform: translateX(-35%) rotateY(0) rotateZ(-12deg) rotateX(0) translateZ(-220px);
  }
}
@keyframes animate-card-image-1 {
  0% {
    opacity: 1;
  }
  25% {
    opacity: 0.3333333333;
  }
  50% {
    opacity: 0.1111111111;
  }
  75% {
    opacity: 0.037037037;
  }
  100% {
    opacity: 0.012345679;
  }
}
@keyframes card-stack-1 {
  0% {
    transform: rotateY(0deg);
  }
  12.5% {
    transform: rotateY(24deg) translateZ(24deg);
  }
  12.5% {
    transform: rotateY(-24deg);
  }
  25% {
    transform: rotateY(0deg);
  }
  37.5% {
    transform: rotateY(-24deg) translateZ(-24deg);
  }
  37.5% {
    transform: rotateY(-24deg);
  }
  50% {
    transform: rotateY(0deg);
  }
  62.5% {
    transform: rotateY(-24deg) translateZ(-24deg);
  }
  62.5% {
    transform: rotateY(-24deg);
  }
  75% {
    transform: rotateY(0deg);
  }
  87.5% {
    transform: rotateY(-24deg) translateZ(-24deg);
  }
  87.5% {
    transform: rotateY(-24deg);
  }
  100% {
    transform: rotateY(0deg);
  }
  112.5% {
    transform: rotateY(-24deg) translateZ(-24deg);
  }
}
.card:nth-child(2) {
  animation: animate2-inactive linear forwards;
  animation-timeline: --scroll-timeline;
}

[data-active-index="1"] .card:nth-child(2) {
  animation: animate2-active linear forwards;
  animation-timeline: --scroll-timeline;
}

.card:nth-child(2) img {
  animation: animate-card-image-2 linear forwards;
  animation-timeline: --scroll-timeline;
}

[data-active-index="1"] .card-stack {
  animation: card-stack-2 linear forwards;
  animation-timeline: --scroll-timeline;
}

.card:nth-child(2)::before {
  animation: card-bg linear forwards;
  animation-timeline: --scroll-timeline;
}

@keyframes animate2-active {
  0% {
    transform: translateX(11%) rotateY(0) rotateZ(6deg) rotateX(0) translateZ(-160px);
  }
  12.5% {
    transform: translateX(116%) rotateY(24deg) rotateZ(0) rotateX(2deg) translateZ(-156px);
  }
  25% {
    transform: translateX(0) rotateY(0) rotateZ(0) rotateX(0) translateZ(0);
  }
  37.5% {
    transform: translateX(-116%) rotateY(-24deg) rotateZ(0) rotateX(2deg) translateZ(-156px);
  }
  50% {
    transform: translateX(-11%) rotateY(0) rotateZ(-6deg) rotateX(0) translateZ(-160px);
  }
  75% {
    transform: translateX(-19%) rotateY(0) rotateZ(-8deg) rotateX(0) translateZ(-180px);
  }
  100% {
    transform: translateX(-27%) rotateY(0) rotateZ(-10deg) rotateX(0) translateZ(-200px);
  }
}
@keyframes animate2-inactive {
  0% {
    transform: translateX(11%) rotateY(0) rotateZ(6deg) rotateX(0) translateZ(-160px);
  }
  25% {
    transform: translateX(0) rotateY(0) rotateZ(0) rotateX(0) translateZ(0);
  }
  50% {
    transform: translateX(-11%) rotateY(0) rotateZ(-6deg) rotateX(0) translateZ(-160px);
  }
  75% {
    transform: translateX(-19%) rotateY(0) rotateZ(-8deg) rotateX(0) translateZ(-180px);
  }
  100% {
    transform: translateX(-27%) rotateY(0) rotateZ(-10deg) rotateX(0) translateZ(-200px);
  }
}
@keyframes animate-card-image-2 {
  0% {
    opacity: 0.3333333333;
  }
  25% {
    opacity: 1;
  }
  50% {
    opacity: 0.3333333333;
  }
  75% {
    opacity: 0.1111111111;
  }
  100% {
    opacity: 0.037037037;
  }
}
@keyframes card-stack-2 {
  0% {
    transform: rotateY(0deg);
  }
  12.5% {
    transform: rotateY(24deg) translateZ(24deg);
  }
  12.5% {
    transform: rotateY(24deg);
  }
  25% {
    transform: rotateY(0deg);
  }
  37.5% {
    transform: rotateY(24deg) translateZ(24deg);
  }
  37.5% {
    transform: rotateY(-24deg);
  }
  50% {
    transform: rotateY(0deg);
  }
  62.5% {
    transform: rotateY(-24deg) translateZ(-24deg);
  }
  62.5% {
    transform: rotateY(-24deg);
  }
  75% {
    transform: rotateY(0deg);
  }
  87.5% {
    transform: rotateY(-24deg) translateZ(-24deg);
  }
  87.5% {
    transform: rotateY(-24deg);
  }
  100% {
    transform: rotateY(0deg);
  }
  112.5% {
    transform: rotateY(-24deg) translateZ(-24deg);
  }
}
.card:nth-child(3) {
  animation: animate3-inactive linear forwards;
  animation-timeline: --scroll-timeline;
}

[data-active-index="2"] .card:nth-child(3) {
  animation: animate3-active linear forwards;
  animation-timeline: --scroll-timeline;
}

.card:nth-child(3) img {
  animation: animate-card-image-3 linear forwards;
  animation-timeline: --scroll-timeline;
}

[data-active-index="2"] .card-stack {
  animation: card-stack-3 linear forwards;
  animation-timeline: --scroll-timeline;
}

.card:nth-child(3)::before {
  animation: card-bg linear forwards;
  animation-timeline: --scroll-timeline;
}

@keyframes animate3-active {
  0% {
    transform: translateX(19%) rotateY(0) rotateZ(8deg) rotateX(0) translateZ(-180px);
  }
  25% {
    transform: translateX(11%) rotateY(0) rotateZ(6deg) rotateX(0) translateZ(-160px);
  }
  37.5% {
    transform: translateX(116%) rotateY(24deg) rotateZ(0) rotateX(2deg) translateZ(-156px);
  }
  50% {
    transform: translateX(0) rotateY(0) rotateZ(0) rotateX(0) translateZ(0);
  }
  62.5% {
    transform: translateX(-116%) rotateY(-24deg) rotateZ(0) rotateX(2deg) translateZ(-156px);
  }
  75% {
    transform: translateX(-11%) rotateY(0) rotateZ(-6deg) rotateX(0) translateZ(-160px);
  }
  100% {
    transform: translateX(-19%) rotateY(0) rotateZ(-8deg) rotateX(0) translateZ(-180px);
  }
}
@keyframes animate3-inactive {
  0% {
    transform: translateX(19%) rotateY(0) rotateZ(8deg) rotateX(0) translateZ(-180px);
  }
  25% {
    transform: translateX(11%) rotateY(0) rotateZ(6deg) rotateX(0) translateZ(-160px);
  }
  50% {
    transform: translateX(0) rotateY(0) rotateZ(0) rotateX(0) translateZ(0);
  }
  75% {
    transform: translateX(-11%) rotateY(0) rotateZ(-6deg) rotateX(0) translateZ(-160px);
  }
  100% {
    transform: translateX(-19%) rotateY(0) rotateZ(-8deg) rotateX(0) translateZ(-180px);
  }
}
@keyframes animate-card-image-3 {
  0% {
    opacity: 0.1111111111;
  }
  25% {
    opacity: 0.3333333333;
  }
  50% {
    opacity: 1;
  }
  75% {
    opacity: 0.3333333333;
  }
  100% {
    opacity: 0.1111111111;
  }
}
@keyframes card-stack-3 {
  0% {
    transform: rotateY(0deg);
  }
  12.5% {
    transform: rotateY(24deg) translateZ(24deg);
  }
  12.5% {
    transform: rotateY(24deg);
  }
  25% {
    transform: rotateY(0deg);
  }
  37.5% {
    transform: rotateY(24deg) translateZ(24deg);
  }
  37.5% {
    transform: rotateY(24deg);
  }
  50% {
    transform: rotateY(0deg);
  }
  62.5% {
    transform: rotateY(24deg) translateZ(24deg);
  }
  62.5% {
    transform: rotateY(-24deg);
  }
  75% {
    transform: rotateY(0deg);
  }
  87.5% {
    transform: rotateY(-24deg) translateZ(-24deg);
  }
  87.5% {
    transform: rotateY(-24deg);
  }
  100% {
    transform: rotateY(0deg);
  }
  112.5% {
    transform: rotateY(-24deg) translateZ(-24deg);
  }
}
.card:nth-child(4) {
  animation: animate4-inactive linear forwards;
  animation-timeline: --scroll-timeline;
}

[data-active-index="3"] .card:nth-child(4) {
  animation: animate4-active linear forwards;
  animation-timeline: --scroll-timeline;
}

.card:nth-child(4) img {
  animation: animate-card-image-4 linear forwards;
  animation-timeline: --scroll-timeline;
}

[data-active-index="3"] .card-stack {
  animation: card-stack-4 linear forwards;
  animation-timeline: --scroll-timeline;
}

.card:nth-child(4)::before {
  animation: card-bg linear forwards;
  animation-timeline: --scroll-timeline;
}

@keyframes animate4-active {
  0% {
    transform: translateX(27%) rotateY(0) rotateZ(10deg) rotateX(0) translateZ(-200px);
  }
  25% {
    transform: translateX(19%) rotateY(0) rotateZ(8deg) rotateX(0) translateZ(-180px);
  }
  50% {
    transform: translateX(11%) rotateY(0) rotateZ(6deg) rotateX(0) translateZ(-160px);
  }
  62.5% {
    transform: translateX(116%) rotateY(24deg) rotateZ(0) rotateX(2deg) translateZ(-156px);
  }
  75% {
    transform: translateX(0) rotateY(0) rotateZ(0) rotateX(0) translateZ(0);
  }
  87.5% {
    transform: translateX(-116%) rotateY(-24deg) rotateZ(0) rotateX(2deg) translateZ(-156px);
  }
  100% {
    transform: translateX(-11%) rotateY(0) rotateZ(-6deg) rotateX(0) translateZ(-160px);
  }
}
@keyframes animate4-inactive {
  0% {
    transform: translateX(27%) rotateY(0) rotateZ(10deg) rotateX(0) translateZ(-200px);
  }
  25% {
    transform: translateX(19%) rotateY(0) rotateZ(8deg) rotateX(0) translateZ(-180px);
  }
  50% {
    transform: translateX(11%) rotateY(0) rotateZ(6deg) rotateX(0) translateZ(-160px);
  }
  75% {
    transform: translateX(0) rotateY(0) rotateZ(0) rotateX(0) translateZ(0);
  }
  100% {
    transform: translateX(-11%) rotateY(0) rotateZ(-6deg) rotateX(0) translateZ(-160px);
  }
}
@keyframes animate-card-image-4 {
  0% {
    opacity: 0.037037037;
  }
  25% {
    opacity: 0.1111111111;
  }
  50% {
    opacity: 0.3333333333;
  }
  75% {
    opacity: 1;
  }
  100% {
    opacity: 0.3333333333;
  }
}
@keyframes card-stack-4 {
  0% {
    transform: rotateY(0deg);
  }
  12.5% {
    transform: rotateY(24deg) translateZ(24deg);
  }
  12.5% {
    transform: rotateY(24deg);
  }
  25% {
    transform: rotateY(0deg);
  }
  37.5% {
    transform: rotateY(24deg) translateZ(24deg);
  }
  37.5% {
    transform: rotateY(24deg);
  }
  50% {
    transform: rotateY(0deg);
  }
  62.5% {
    transform: rotateY(24deg) translateZ(24deg);
  }
  62.5% {
    transform: rotateY(24deg);
  }
  75% {
    transform: rotateY(0deg);
  }
  87.5% {
    transform: rotateY(24deg) translateZ(24deg);
  }
  87.5% {
    transform: rotateY(-24deg);
  }
  100% {
    transform: rotateY(0deg);
  }
  112.5% {
    transform: rotateY(-24deg) translateZ(-24deg);
  }
}
.card:nth-child(5) {
  animation: animate5-inactive linear forwards;
  animation-timeline: --scroll-timeline;
}

[data-active-index="4"] .card:nth-child(5) {
  animation: animate5-active linear forwards;
  animation-timeline: --scroll-timeline;
}

.card:nth-child(5) img {
  animation: animate-card-image-5 linear forwards;
  animation-timeline: --scroll-timeline;
}

[data-active-index="4"] .card-stack {
  animation: card-stack-5 linear forwards;
  animation-timeline: --scroll-timeline;
}

.card:nth-child(5)::before {
  animation: card-bg linear forwards;
  animation-timeline: --scroll-timeline;
}

@keyframes animate5-active {
  0% {
    transform: translateX(35%) rotateY(0) rotateZ(12deg) rotateX(0) translateZ(-220px);
  }
  25% {
    transform: translateX(27%) rotateY(0) rotateZ(10deg) rotateX(0) translateZ(-200px);
  }
  50% {
    transform: translateX(19%) rotateY(0) rotateZ(8deg) rotateX(0) translateZ(-180px);
  }
  75% {
    transform: translateX(11%) rotateY(0) rotateZ(6deg) rotateX(0) translateZ(-160px);
  }
  87.5% {
    transform: translateX(116%) rotateY(24deg) rotateZ(0) rotateX(2deg) translateZ(-156px);
  }
  100% {
    transform: translateX(0) rotateY(0) rotateZ(0) rotateX(0) translateZ(0);
  }
  112.5% {
    transform: translateX(-116%) rotateY(-24deg) rotateZ(0) rotateX(2deg) translateZ(-156px);
  }
}
@keyframes animate5-inactive {
  0% {
    transform: translateX(35%) rotateY(0) rotateZ(12deg) rotateX(0) translateZ(-220px);
  }
  25% {
    transform: translateX(27%) rotateY(0) rotateZ(10deg) rotateX(0) translateZ(-200px);
  }
  50% {
    transform: translateX(19%) rotateY(0) rotateZ(8deg) rotateX(0) translateZ(-180px);
  }
  75% {
    transform: translateX(11%) rotateY(0) rotateZ(6deg) rotateX(0) translateZ(-160px);
  }
  100% {
    transform: translateX(0) rotateY(0) rotateZ(0) rotateX(0) translateZ(0);
  }
}
@keyframes animate-card-image-5 {
  0% {
    opacity: 0.012345679;
  }
  25% {
    opacity: 0.037037037;
  }
  50% {
    opacity: 0.1111111111;
  }
  75% {
    opacity: 0.3333333333;
  }
  100% {
    opacity: 1;
  }
}
@keyframes card-stack-5 {
  0% {
    transform: rotateY(0deg);
  }
  12.5% {
    transform: rotateY(24deg) translateZ(24deg);
  }
  12.5% {
    transform: rotateY(24deg);
  }
  25% {
    transform: rotateY(0deg);
  }
  37.5% {
    transform: rotateY(24deg) translateZ(24deg);
  }
  37.5% {
    transform: rotateY(24deg);
  }
  50% {
    transform: rotateY(0deg);
  }
  62.5% {
    transform: rotateY(24deg) translateZ(24deg);
  }
  62.5% {
    transform: rotateY(24deg);
  }
  75% {
    transform: rotateY(0deg);
  }
  87.5% {
    transform: rotateY(24deg) translateZ(24deg);
  }
  87.5% {
    transform: rotateY(24deg);
  }
  100% {
    transform: rotateY(0deg);
  }
  112.5% {
    transform: rotateY(24deg) translateZ(24deg);
  }
}
@keyframes theme-bg {
  0% {
    background-color: #471703;
  }
  25% {
    background-color: #282624;
  }
  50% {
    background-color: #212e14;
  }
  75% {
    background-color: #184152;
  }
  100% {
    background-color: #162432;
  }
}
@keyframes card-bg {
  0% {
    background-color: #471703;
  }
  25% {
    background-color: #282624;
  }
  50% {
    background-color: #212e14;
  }
  75% {
    background-color: #184152;
  }
  100% {
    background-color: #162432;
  }
}
.warning {
  position: absolute;
  bottom: 24px;
  left: 0;
  right: 0;
  text-align: center;
  white-space: nowrap;
  opacity: 0;
  transition: 300ms opacity;
}
.warning span {
  display: inline-flex;
  font-size: 12px;
  height: 28px;
  align-items: center;
  color: white;
  padding: 0 12px;
  border-radius: 14px;
  font-weight: 500;
  background-color: rgba(0, 0, 0, 0.66);
}

.warning.show {
  opacity: 1;
}

.explainer {
  position: absolute;
  right: 12px;
  top: 12px;
  background-color: transparent;
  width: 300px;
  color: white;
  padding: 24px;
  padding-right: 40px;
  display: none;
  z-index: 9;
}

.explainer input, .explainer div {
  position: absolute;
  top: 8px;
  right: 8px;
  appearance: none;
  width: 30px;
  height: 30px;
}

.explainer div {
  display: flex;
  align-items: center;
  justify-content: center;
  pointer-events: none;
  border-radius: 50%;
}

.explainer div svg {
  width: 24px;
  opacity: 0.5;
}

.explainer:has(input:checked) div::before {
  content: "×";
  font-size: 20px;
}

.explainer:has(input:checked) div svg {
  opacity: 0;
}

.explainer p {
  display: none;
}

.explainer:has(input:checked) p {
  display: block;
}

.explainer:has(input:checked) {
  background-color: black;
}

.explainer a {
  color: inherit;
  font-family: inherit;
}

.explainer p {
  font-family: ui-monospace, SFMono-Regular, "SF Mono", Menlo, Consolas, "Liberation Mono", monospace;
  font-size: 12px;
  line-height: 18px;
}

.explainer p ~ p {
  margin-top: 1em;
}

@media (min-width: 768px) {
  .explainer {
    display: block;
  }

  .device {
    border-radius: 40px;
    box-shadow: 0 0 0 6px #141414;
  }
}

@use "sass:math";

$card-count: 5;
$step-distance: (100 / ($card-count - 1));
$half-step-distance: ($step-distance / 2);
$theme-body-bg: #471703, #282624, #212e14, #184152, #162432;
$theme-card-bg: #471703, #282624, #212e14, #184152, #162432;

:root {
  font-family: Inter, system-ui, Avenir, Helvetica, Arial, sans-serif;
  line-height: 1.5;
  font-weight: 400;
  --dim-card-width: 300px;
  --dim-card-height: 400px;
  --dim-card-border-radius: 16px;
  --box-shadow-card: 0 1px 12px rgba(0, 0, 0, 0.4);
}

::-webkit-scrollbar {
  display: none;
}

* {
  box-sizing: border-box;
}

body,
html {
  margin: 0;
  padding: 0;
}

body {
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #ddd;
  height: 100vh;
  min-height: 800px;
  timeline-scope: --scroll-timeline;
  animation: theme-bg linear forwards;
  animation-timeline: --scroll-timeline;
}

main {
  width: 800px;
  height: 600px;
  perspective: 1000px;
  transform-style: preserve-3d;
}

.scroller {
  width: 100%;
  height: 100%;
  overflow: auto;
  white-space: nowrap;
  display: flex;
  scroll-snap-type: x mandatory;
  scroll-timeline: --scroll-timeline;
  scroll-timeline-axis: x;
}

.scroll-item {
  flex: 0 0 100%;
  height: 100%;
  scroll-snap-align: start;
}

[data-debug="true"] .scroll-item {
  outline: 1px dashed magenta;
}

.card-stack {
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  transform-style: preserve-3d;
  pointer-events: none;
}

.card {
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  margin: auto;
  width: var(--dim-card-width);
  height: var(--dim-card-height);
  border-radius: var(--dim-card-border-radius);
  display: flex;
  align-items: center;
  justify-content: center;
  transform-style: preserve-3d;
  overflow: hidden;
  background-color: rgba(255, 255, 255, 0.8);
  box-shadow: var(--box-shadow-card);
}

.card img {
  position: absolute;
  object-fit: cover;
  width: 100%;
  z-index: 1;
  height: 100%;
}

.card::before {
  position: absolute;
  top: -4px;
  bottom: -4px;
  right: -4px;
  left: -4px;
  content: "";
}

@mixin card-active {
  transform: translateX(0) rotateY(0) rotateZ(0) rotateX(0) translateZ(0);
}

@mixin card-exiting-to-left {
  transform: translateX(-116%) rotateY(-24deg) rotateZ(0) rotateX(2deg)
    translateZ(-156px);
}

@mixin card-exiting-to-right {
  transform: translateX(116%) rotateY(24deg) rotateZ(0) rotateX(2deg)
    translateZ(-156px);
}

@mixin card-exited-to-left($steps) {
  $rotateZ: -4 + ($steps * -2);
  $translateX: -3 - ($steps * 8);
  $translateZ: -140 - ($steps * 20);
  transform: translateX($translateX * 1%) rotateY(0) rotateZ($rotateZ * 1deg)
    rotateX(0) translateZ($translateZ * 1px);
}

@mixin card-exited-to-right($steps) {
  $rotateZ: 4 + ($steps * 2);
  $translateX: 3 + ($steps * 8);
  $translateZ: -140 - ($steps * 20);
  transform: translateX($translateX * 1%) rotateY(0) rotateZ($rotateZ * 1deg)
    rotateX(0) translateZ($translateZ * 1px);
}

@mixin animate-active($index) {
  @keyframes animate#{$index}-active {
    @for $i from 0 through $card-count - 1 {
      $percentage: $step-distance * $i;
      $active: $i == $index - 1;
      $steps: $i - ($index - 1);

      @if not $active {
        #{$percentage * 1%} {
          @if $steps > 0 {
            @include card-exited-to-left($steps);
          } @else {
            @include card-exited-to-right((0 - $steps));
          }
        }
      }

      @if ($active) {
        @if $i > 0 {
          #{($percentage - $half-step-distance) * 1%} {
            @include card-exiting-to-right;
          }
        }

        #{$percentage * 1%} {
          @include card-active;
        }

        #{($percentage + $half-step-distance) * 1%} {
          @include card-exiting-to-left;
        }
      }
    }
  }
}

@mixin animate-inactive($index) {
  @keyframes animate#{$index}-inactive {
    @for $i from 0 through $card-count - 1 {
      $percentage: $step-distance * $i;
      $active: $i == $index - 1;
      $steps: $i - ($index - 1);

      @if not $active {
        #{$percentage * 1%} {
          @if $steps > 0 {
            @include card-exited-to-left($steps);
          } @else {
            @include card-exited-to-right((0 - $steps));
          }
        }
      }

      @if ($active) {
        #{$percentage * 1%} {
          @include card-active;
        }
      }
    }
  }
}

@mixin card-stack-keyframes($index) {
  @keyframes card-stack-#{$index} {
    @for $i from 0 through $card-count - 1 {
      $percentage: $step-distance * $i;
      $steps: $i - ($index - 1);
      $rotate: if($steps > 0, -24deg, 24deg);

      @if $i > 0 {
        #{($percentage - $half-step-distance) * 1%} {
          transform: rotateY($rotate);
        }
      }

      #{$percentage * 1%} {
        transform: rotateY(0deg);
      }

      #{($percentage + $half-step-distance) * 1%} {
        transform: rotateY($rotate) translateZ($rotate);
      }
    }
  }
}

@mixin animate-card-image($index) {
  @keyframes animate-card-image-#{$index} {
    @for $i from 0 through $card-count - 1 {
      $percentage: $step-distance * $i;
      $active: $i == $index - 1;
      $steps: $i - ($index - 1);
      $opacity: 1 / (math.pow(3, abs($steps)));

      #{$percentage * 1%} {
        opacity: $opacity;
      }
    }
  }
}

@for $i from 1 through $card-count {
  .card:nth-child(#{$i}) {
    animation: animate#{$i}-inactive linear forwards;
    animation-timeline: --scroll-timeline;
  }

  [data-active-index="#{$i - 1}"] .card:nth-child(#{$i}) {
    animation: animate#{$i}-active linear forwards;
    animation-timeline: --scroll-timeline;
  }

  .card:nth-child(#{$i}) img {
    animation: animate-card-image-#{$i} linear forwards;
    animation-timeline: --scroll-timeline;
  }

  [data-active-index="#{$i - 1}"] .card-stack {
    animation: card-stack-#{$i} linear forwards;
    animation-timeline: --scroll-timeline;
  }

  .card:nth-child(#{$i})::before {
    animation: card-bg linear forwards;
    animation-timeline: --scroll-timeline;
  }

  @include animate-active($i);
  @include animate-inactive($i);
  @include animate-card-image($i);
  @include card-stack-keyframes($i);
}

// Back ground theme
@keyframes theme-bg {
  @for $i from 1 through $card-count {
    $percentage: $step-distance * ($i - 1);

    #{$percentage * 1%} {
      background-color: nth($theme-body-bg, $i);
    }
  }
}

// Back ground theme
@keyframes card-bg {
  @for $i from 1 through $card-count {
    $percentage: $step-distance * ($i - 1);

    #{$percentage * 1%} {
      background-color: nth($theme-card-bg, $i);
    }
  }
}

// -----------------------------------
// Styles for the demo explainer only

.warning {
  position: absolute;
  bottom: 24px;
  left: 0;
  right: 0;
  text-align: center;
  white-space: nowrap;
  opacity: 0;
  transition: 300ms opacity;
  
  span {
    display: inline-flex;
    font-size: 12px;
    height: 28px;
    align-items: center;
    color: white;
    padding: 0 12px;
    border-radius: 14px;
    font-weight: 500;
    background-color: rgba(0, 0, 0, 0.66);
  }
}

.warning.show {
  opacity: 1;
}

.explainer {
  position: absolute;
  right: 12px;
  top: 12px;
  background-color: transparent;
  width: 300px;
  color: white;
  padding: 24px;
  padding-right: 40px;
  display: none;
  z-index: 9;
}

.explainer input, .explainer div {
  position: absolute;
  top: 8px;
  right: 8px;
  appearance: none;
  width: 30px;
  height: 30px;
}

.explainer div {
  display: flex;
  align-items: center;
  justify-content: center;
  pointer-events: none;
  border-radius: 50%;
}

.explainer div svg {
  width: 24px;
  opacity: 0.5;
}

.explainer:has(input:checked) div::before {
  content: '×';
  font-size: 20px;
}
.explainer:has(input:checked) div svg {
  opacity: 0;
}

.explainer p {
  display: none;
}

.explainer:has(input:checked) p {
  display: block;
}

.explainer:has(input:checked) {
  background-color: black;
}

.explainer a {
  color: inherit;
  font-family: inherit;
}

.explainer p {
  font-family: ui-monospace, SFMono-Regular, "SF Mono", Menlo, Consolas, "Liberation Mono", monospace;
  font-size: 12px;
  line-height: 18px;
}

.explainer p ~ p {
  margin-top: 1em;
}

@media (min-width: 768px) {
  .explainer {
    display: block;
  }
  
  .device {
    border-radius: 40px;
    box-shadow: 0 0 0 6px rgb(20, 20, 20);
  }
}

main.js

const main = document.querySelector("main");

document.querySelector(".scroller").addEventListener("scrollsnapchange", (event) => {
  main.dataset.activeIndex = Math.round(event.target.scrollLeft / main.getBoundingClientRect().width);
});

```
## OUTPUT:
![alt text](<Screenshot (33).png>)
![alt text](<Screenshot (34).png>)

## RESULT:
The program for designing an interactive image gallery using HTML, CSS and JavaScript is executed successfully.
