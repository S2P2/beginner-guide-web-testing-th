# Module 6: Organizing Tests for Growth

!!! warning
    AI generated content, no human review yet

### 🎯 Objective

In this module, you will learn best practices for organizing your tests to make them clean, maintainable, and scalable. You will move beyond writing single scripts and begin to think about structuring a full test suite using industry-standard patterns.

###  📝 Lesson Plan

| Topic | Description | Duration |
| :--- | :--- | :--- |
| **Grouping Tests: `describe` and `it`** | Explain how to use these blocks to create a readable test structure. | 20 mins |
| **Staying DRY with Hooks: `beforeEach`** | Demonstrate how `beforeEach` can remove duplicate setup code (like `cy.visit()`). | 30 mins |
| **Intro to the Page Object Model (POM)** | High-level conceptual overview of POM. Explain its value for maintainability but keep it simple. | 30 mins |
| **Lab: Refactor Your Test** | Students refactor their "Text Box" test to use `describe`, `it`, and `beforeEach`. | 40 mins |
| **Q&A** | Discussion on when to use these patterns. | 10 mins |

### 📖 Content

As you write more tests, you'll find yourself repeating code and your files will get messy. Let's learn two simple patterns to keep your test suite clean and easy to manage.

#### 1. Grouping Tests with `describe` and `it`

Most testing frameworks use `describe` and `it` blocks to structure tests.
*   **`describe('a feature', ...)`:** A `describe` block is a container for a group of related tests. For example, you might have a `describe` block for "Login Page Tests" or "Profile Form Tests."
*   **`it('should do something', ...)`:** An `it` block contains the actual test code for one specific scenario. The description should clearly state what the test is supposed to do.

This creates a beautiful, readable output when you run your tests.

```javascript
// A "describe" block groups tests for the Forms feature
describe('DemoQA Forms', () => {

  // A specific test for the text box
  it('should successfully submit the text box form', () => {
    // Arrange, Act, Assert code goes here...
  });

  // Another specific test for the check box
  it('should allow a user to select a checkbox', () => {
    // Arrange, Act, Assert code for the checkbox test...
  });
});
```

#### 2. Avoiding Repetition with Hooks (`beforeEach`)

What if every test in your `describe` block needs to visit the same URL first? You could copy `await page.goto(...)` into every `it` block, but that's repetitive.

A **hook** is a function that runs automatically before or after your tests. The most common one is `beforeEach`.

*   **`beforeEach(...)`:** This function will run once *before each `it` block* inside its `describe` block. It's perfect for setup code.

**Example:**

---
##### <tabs>
<tab label="Playwright / Cypress">
```javascript
describe('Text Box Page', () => {
  // This will run before EACH of the 'it' blocks below
  beforeEach(async ({ page }) => { // or just beforeEach(() => { for Cypress
    // 1. Arrange: Go to the page
    await page.goto('https://demoqa.com/text-box'); // cy.visit(...) for Cypress
  });

  it('should submit a complete form', () => {
    // No need to visit the URL here!
    // 2. Act
    // 3. Assert
  });

  it('should show an error with an invalid email', () => {
    // No need to visit the URL here either!
    // 2. Act
    // 3. Assert
  });
});
```
</tab>
<tab label="Selenium (with Mocha)">
```javascript
describe('Text Box Page', function () {
  let driver;

  // This runs before all tests in the block
  before(async function () {
    driver = await new Builder().forBrowser('chrome').build();
  });

  // This runs before EACH test
  beforeEach(async function() {
      await driver.get('https://demoqa.com/text-box');
  });

  it('should submit a complete form', async function () {
    // Test code...
  });

  after(async () => await driver.quit());
});
```
</tab>
</tabs>

---

#### 3. The "Pro" Way: The Page Object Model (POM) - A Brief Intro

When you have dozens of tests for the same page, you might have the selector for the "Submit" button (`#submit`) repeated in 20 different files. What happens if a developer changes that ID? You have to fix it in 20 places!

The **Page Object Model (POM)** is a design pattern that solves this. It's simple:
*   You create a separate class or object for each page of your application.
*   This object holds all the selectors and complex functions related to that page.
*   Your tests then *use* this object instead of putting raw selectors directly in the test code.

**Conceptual Example (Not for coding yet):**

```javascript
// textBoxPage.js - A Page Object
class TextBoxPage {
  constructor(page) {
    this.fullNameInput = page.locator('#userName');
    this.submitButton = page.locator('#submit');
  }

  async submitForm(name, email) {
    await this.fullNameInput.type(name);
    // ... type email
    await this.submitButton.click();
  }
}

// myTest.spec.js - The Test
test('should submit the form', async ({ page }) => {
  const textBoxPage = new TextBoxPage(page);
  await page.goto(...);
  await textBoxPage.submitForm('John Doe', 'test@test.com');
  // ... assertions
});
```

**Benefits:**
*   **Maintainable:** If a selector changes, you only fix it in **one** place (the Page Object).
*   **Readable:** Test scripts become cleaner and describe *what* they are doing, not *how* they are doing it (`textBoxPage.submitForm(...)` is easier to read than a series of `type` and `click` commands).

We won't be building a full POM in this beginner's course, but it's the most important concept to learn as you start building a real-world test suite.
