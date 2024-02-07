# Project Summary

In this project, we'll introduce you to vanilla JS DOM manipulation by creating a small project. The basic HTML and CSS have been provided for you, and you will be adding in the Javascript to make the interface interactive. The goal of this project is to create a simple counter interface that can use three different themes.

### Step 1

#### Summary

In this step, we'll create our Javascript file and connect it to our HTML.

#### Instructions

- Create a new file called `index.js`.
- Add a `console.log('hello world')` so we can see if the script is running.
- Open `index.html`
- Inside the `<body>` tag, but after the `<main>` element, add a `<script>` tag to bring in your `index.js` file.

#### Solution

<details>
<summary>
<code>/index.html</code>
</summary>

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Theme Changing Counter</title>
    <link rel="stylesheet" href="./index.css" />
    <link rel="stylesheet" href="./themes.css" />
  </head>
  <body>
    <header>
      <p>Choose a theme:</p>

      <button>Facebook</button> <button>DevMountain</button>
      <button>Twitter</button> <button>Default</button>
    </header>
    <main>
      <h1>0</h1>
      <h2>Clicks</h2>
      <section>
        <button>-</button> <button>Reset</button> <button>+</button>
      </section>
    </main>
    <script src="./index.js"></script>
  </body>
</html>
```

</details>

### Step 2

#### Summary

In this step, we'll start working on the Javascript functions needed for the counter functionality in `index.js`

#### Instructions

- Create a global variable called `count` with an initial value of `0`. We will update this global variable in all of our functions.
- Next, create a function called `increase` that increases the value of `count` by 1. For now, `console.log` the new value of count so you can see when the function runs.
- Follow the same pattern to create a function called `decrease` that decreases the value of `count` by 1 and `reset` that resets the value of `count` to 0.

#### Solution

<details>
<summary>
<code>/index.js</code>
</summary>

```js
let count = 0;

function increase() {
  count++;
  console.log(count);
}

function decrease() {
  count--;
  console.log(count);
}

function reset() {
  count = 0;
  console.log(count);
}
```

</details>

### Step 3

#### Summary

In this step, we will add event listeners to run our Javascript functions when the buttons are clicked.

#### Instructions

- In `index.html`, find the `h1` element and add an `id` attribute with a value of `"counter"`.
  - We need an `id` for this element so we can update its text in Javascript in the next step.
- We need an `id` for each button we will use that affects the counter. In `index.html` add an `id` to each button, `sub`, `reset`, and `add`.
  - We need to add event listeners to the `-`, `reset`, and `+` buttons that will use our `increase`, `reset`, and `decrease` functions as the call back.
  - Use `document.querySelectorAll` to select all buttons inside the section and assign that value to a new variable called `counterBtns`
  - Remember that `querySelectorAll` returns a node that works like an array. Create a for loop that will loop through each button element, check the `id`, and then add an event listener using the correct function for each button.

#### Solution

<details>
<summary>
<code>/index.html</code></summary>

```js

const counterBtns = document.querySelectorAll("section button");

for (let i = 0; i < counterBtns.length; i++) {
  if (counterBtns[i].id === "sub") {
    counterBtns[i].addEventListener("click", decrease);
  } else if (counterBtns[i].id === "reset") {
    counterBtns[i].addEventListener("click", reset);
  } else {
    counterBtns[i].addEventListener("click", increase);
  }
}

```

</details>

### Step 4

#### Summary

In this step, we will update our Javascript functions to update the content in the `h1` instead of displaying `count` in the console.

#### Instructions

- In `index.js`, use `document.querySelector` to create a new variable called `element` that references the `h1` element with an id of `counter` from `index.html`
- In your `increase`, `decrease`, and `reset` functions, use the `textContent` property of the `element` variable to change the value that is displayed in the `h1` with the new value of `count`.
- Remove your `console.log` in each function.

#### Solution

<details>
<summary>
<code>/index.js</code>
</summary>

```js
let count = 0;
const element = document.querySelector("#counter");

function increase() {
  count++;
  element.innerText = count;
}

function decrease() {
  count--;
  element.innerText = count;
}

function reset() {
  count = 0;
  element.innerText = count;
}
```

</details>

### Step 5

#### Summary

In this step, we will start working on the javascript functions needed to change the themes on the page. The themes are already provided for you in `themes.css` and do not need to be changed. Instead, we just need to add the correct class name to the `body`, `main` and `button` elements.

#### Instructions

- In `index.js`, create a function called `selectTheme` that takes in a string called `theme` as a parameter.
- Use `document.querySelector` to select the `body` element and change its `className` property to the `theme` variable.
- Repeat this step for the `main` element.
- We will need to select all of the buttons in the `index.html` file. We can use `document.querySelectorAll` to select all of them and assign them to a global variable called `themeBtns`. We will to use a `for` loop to change the `className` property for every `button` element in the themeBtns variable. Remember, when selecting elements with `document.querySelectorAll`, it returns a `NodeList` which is an array-like list.

#### Solution

<details><summary><code>/index.js</code></summary>

```js
const themeBtns = document.querySelectorAll("header button");

function selectTheme(theme) {
  document.querySelector("body").className = theme;
  document.querySelector("main").className = theme;

  for (let i = 0; i < themeBtns.length; i++) {
    themeBtns[i].className = theme;
  }
}
```

</details>

### Step 6

#### Summary

In this final step, we will update our Javascript to run the `selectTheme` function and pass in the appropriate parameter when a theme button is pressed.

#### Instructions

- In `index.js`, add event listeners to each `button` inside the `header` element. 
- Create a `for loop` that will loop through the variable `themeBtns` and add an event listener to each button. The callback function should use a conditional to check the `textContent` of each `button` and invoke the `selectTheme` function, passing the correlating theme as the `argument`.

#### Solution

<details><summary><code>/index.html</code></summary>

```js
for (let i = 0; i < themeBtns.length; i++) {
  themeBtns[i].addEventListener("click", () => {
    if (themeBtns[i].textContent === "Facebook") {
        selectTheme("facebook");
      } else if (themeBtns[i].textContent === "Twitter") {
        selectTheme("twitter");
      } else if (themeBtns[i].textContent === "DevMountain") {
        selectTheme("devmountain");
      } else {
        selectTheme("default");
      }
  });
}
```

</details>
