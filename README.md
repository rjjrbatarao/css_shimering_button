# css_shimering_button
Modified to trigger shining shimering using javascript.
```html
<main id="app">

    <button id="demo">
        <span class="text">SHINING SHIMERING</span>
        <span class="shimmer"></span>
    </button>
    
</main>
```
```css

:root {
    --glow-hue: 222deg;
    --shadow-hue: 180deg;
    --spring-easing: linear(
    0, 0.002, 0.01 0.9%, 0.038 1.8%, 0.156, 0.312 5.8%, 0.789 11.1%, 1.015 14.2%,
    1.096, 1.157, 1.199, 1.224 20.3%, 1.231, 1.231, 1.226, 1.214 24.6%,
    1.176 26.9%, 1.057 32.6%, 1.007 35.5%, 0.984, 0.968, 0.956, 0.949 42%,
    0.946 44.1%, 0.95 46.5%, 0.998 57.2%, 1.007, 1.011 63.3%, 1.012 68.3%,
    0.998 84%, 1
  );
    --spring-duration: 1.33s;
}
@property --shimmer {
    syntax: "<angle>";
    inherits: false;
    initial-value: 33deg;
}

@keyframes shimmer {
    0% {
        --shimmer: 0deg;
    }
    100% {
        --shimmer: 360deg;
    }
}

@keyframes shine {
    0% {
        opacity: 0;
    }
    15% {
        opacity: 1;
    }
    55% {
        opacity: 1;
    }
    100% {
        opacity: 0;
    }
}

button {
    font-weight: 600;
    background-color: transparent;
    padding: .8em 1.4em;
    position: relative;
    isolation: isolate;
    border-radius: 0.66em;
    scale: 1;
    transition: all var(--spring-duration) var(--spring-easing);
}


.shimmer {
    position: absolute;
    inset: -40px;
    border-radius: inherit;
    mask-image: conic-gradient(
        from var(--shimmer, 0deg),
        transparent 0%,
        transparent 10%,
        black 36%,
        black 45%,
        transparent 50%,
        transparent 60%,
        black 85%,
        black 95%,
        transparent 100%
    );
    mask-size: cover;
    mix-blend-mode: plus-lighter;
    animation: shimmer 1s linear infinite both;
}


button.active .shimmer::before,
button.active .shimmer::after {
    opacity: 1;
    animation: shine 1.2s ease-in 1 forwards;
}
.shimmer::before,
.shimmer::after {
    transition: all 0.5s ease;
    opacity: 0;
    content: "";
    border-radius: inherit;
    position: absolute;
    mix-blend-mode: color;
    inset: 40px;
    pointer-events: none;
}
.shimmer::before {
    box-shadow: 0 0 3px 2px hsl(var(--glow-hue) 20% 95%),
        0 0 7px 4px hsl(var(--glow-hue) 20% 80%),
        0 0 13px 4px hsl(var(--glow-hue) 50% 70%),
        0 0 25px 5px hsl(var(--glow-hue) 100% 70%);
    z-index: -1;
}
.shimmer::after {
    box-shadow: inset 0 0 0 1px hsl(var(--glow-hue) 70% 95%),
        inset 0 0 2px 1px hsl(var(--glow-hue) 100% 80%),
        inset 0 0 5px 2px hsl(var(--glow-hue) 100% 70%);
    z-index: 2;
}

body,
html {
    display: flex;
    height: 100vh;
    padding: 0;
    /*     background: radial-gradient(circle at 50% 0%, #9588c7 15%, #c79ed5 75%); */
    background-image: radial-gradient(
        circle at 50% 0%,
        rgb(67, 54, 74) 16.4%,
        rgb(47, 48, 67) 68.2%,
        rgb(27, 23, 36) 99.1%
    );
}
main#app {
    height: 100vh;
    width: 100vw;
    display: flex;
    align-items: center;
    justify-content: center;
}

```
```js
var current = document.getElementById("demo");
var inverse = false;
setInterval(()=>{
  if(inverse){
    current.classList.add("active");
  } else {
    current.classList.remove("active");
  }
  inverse = !inverse;
},1500);
```
## Original Sources
https://www.buttons.cool/button/gOqNxRa
