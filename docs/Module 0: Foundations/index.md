# Module 0: Foundations

## 📝 Lesson Plan

This module is designed for you to complete at your own pace. Follow these steps to build your foundational knowledge.

| Step | Your Goal & Activity | Estimated Time |
| :--- | :--- | :--- |
| **1. Getting Started** | Read the module objective. Take a moment to reflect on what you personally want to achieve with this new skill. | 2 mins |
| **2. Understand a Website's Structure** | Learn the three core components of a website by reading the "House Analogy" section. Your goal is to understand the different roles of HTML, CSS, and JavaScript. | 5 mins |
| **3. Learn the Bare Minimum Code** | Study the four essential programming concepts: Variables, Strings, Functions, and Async/Await. Try to understand the purpose of each code example. | 5 mins |
| **4. Knowledge Check** | Review the key concepts from this module. Can you explain the House Analogy and the four programming concepts in your own words? Jot down any points you're unsure about to revisit. | 5 mins |

## 🎯 Objective

Your objective in this module is to establish a foundational understanding of how websites function and grasp the essential programming concepts required for test automation. We'll ensure that even if you're an absolute beginner, you'll build a clear mental model before you start writing any code.

## 📖 Content

### What is a Website? The House Analogy

Before we can test a website, we need to know what it's made of. Think of a website like a house:

<figure markdown="span">
    ![HTML-CSS-JS](https://www.keentodesign.com.au/cdn-cgi/imagedelivery/eOylWWvDYZyJkbAUtQZpuQ/www.keentodesign.com.au/html.png/w=768)
    <figcaption>source: https://www.keentodesign.com.au/difference-between-css-html-and-javascript/</figcaption>
</figure>

*   **HTML (HyperText Markup Language) is the Structure.** It's the foundation, the walls, the roof, and the doorways. It gives the house its shape. Without it, there's just an empty plot of land. In a website, HTML creates the buttons, forms, and text boxes.
    ```html
    <!-- This is the "door" -->
    <button id="submitButton">Click Me</button>
    ```

*   **CSS (Cascading Style Sheets) is the Style.** It's the paint color, the furniture, and the decorations. It makes the house look good. In a website, CSS controls the colors, fonts, and layout.
    ```css
    /* This makes our "door" blue */
    #submitButton {
      background-color: #007bff;
      color: white;
    }
    ```

*   **JavaScript (JS) is the Function.** It's the electricity, the plumbing, and the garage door opener. It makes the house *do things*. When you flip a switch, the lights turn on. On a website, JavaScript handles what happens when you click a button, submit a form, or interact with the page.

Our job in test automation is to be the "home inspector." We don't need to be the architect (HTML), the interior designer (CSS), or the electrician (JS), but we *do* need to know how to open the doors, flip the switches, and check that everything works as expected.

### What Programming Do I Need? The Bare Minimum

You do not need to be a professional developer to write tests! You only need to grasp a few core concepts. Think of them as your basic toolkit.

1.  **Variables: The Labeled Boxes**
    A variable is just a container with a label that holds something. We use it to store information we want to use later.
    ```javascript
    // 'userName' is the label on a box holding the text "John Doe"
    let userName = "John Doe";
    ```

2.  **Strings: The Text**
    A "string" is just the official name for a piece of text. We wrap it in quotes.
    ```javascript
    let greeting = "Hello, World!";
    ```

3.  **Functions: The Reusable Recipes**
    A function is a named set of instructions that you can run whenever you want. This saves you from writing the same code over and over.
    ```javascript
    // This is the recipe for greeting someone
    function greet(name) {
      console.log("Hello, " + name);
    }

    // Now we use the recipe!
    greet("Alice"); // Prints "Hello, Alice"
    greet("Bob");   // Prints "Hello, Bob"
    ```

4.  **Async/Await: The "Wait Your Turn" Keywords**
    This is the trickiest, but most important, concept. Websites don't load instantly. When you click a button, you might have to wait for something to happen. `async` and `await` are special keywords that tell our test script: "Hey, this next step might take a moment. **Wait** for it to finish before you move on."

    ```javascript
    // 'async' tells JavaScript to expect some waiting inside this function
    async function submitForm() {
      // 'await' pauses here until the button is clicked and the page responds
      await page.click("#submitButton");

      // This line will NOT run until the click is complete
      console.log("Button has been clicked!");
    }
    ```
    Nearly every test you write will use `async/await`!


### ➡️ Next: Building the House for Real — HTML & DOM

Now that you understand the basic building blocks of a website, it’s time to **see the house blueprint up close**.
In the next lesson, we’ll open the hood on real HTML, explore how the browser turns it into a living structure called the **DOM**, and learn your first hands-on testing skill: **Inspecting Elements**.
