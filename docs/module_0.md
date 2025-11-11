# Module 0: The Absolute Basics - Laying the Foundation

### 🎯 Objective

Your objective in this module is to establish a foundational understanding of how websites function and grasp the essential programming concepts required for test automation. We'll ensure that even if you're an absolute beginner, you'll build a clear mental model before you start writing any code.

### 📝 Lesson Plan

| Topic | Description | Duration |
| :--- | :--- | :--- |
| **Welcome & Icebreaker** | Instructor introduction, brief student intros (What's your role? What do you hope to learn?). | 15 mins |
| **What is a Website?** | The "House" analogy. | 20 mins |
| **What Programming Do I Need?** | The "Bare Minimum" concepts. | 45 mins |
| **Q&A** | Open floor for questions. | 10 mins |

### 📖 Content

#### What is a Website? The House Analogy

Before we can test a website, we need to know what it's made of. Think of a website like a house:

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

#### What Programming Do I Need? The Bare Minimum

You do not need to be a professional developer to write tests! You only need a few core concepts. Think of them as your basic toolkit.

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
