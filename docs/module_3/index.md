# Module 3: The 3 Core Building Blocks of Automation

### 🎯 Objective

In this crucial hands-on module, you will master the "Find, Act, Assert" pattern and gain practical experience writing the three fundamental lines of any test. The interactive code-switcher will be an essential tool to help you apply these concepts across different frameworks.

### 📝 Lesson Plan

| Topic | Description | Duration |
| :--- | :--- | :--- |
| **The "Find, Act, Assert" Mantra** | Introduce the core pattern. "First you find the thing, then you do something to it, then you check the result." | 15 mins |
| **1. Selectors: Finding the Element** | Explain different strategies (ID, class, text) with live examples on `demoqa.com`. | 30 mins |
| **2. Actions: Interacting with It** | Demonstrate `.click()` and `.type()` on the "Text Box" and "Buttons" pages. | 20 mins |
| **3. Assertions: Checking the Result**| Show how to check for visibility or text content. | 20 mins |
| **Lab: The Building Blocks** | Students write 3 separate "mini-tests," one for each concept, using the code-switcher for reference. | 45 mins |
| **Q&A and Troubleshooting** | Review student code and answer questions. | 15 mins |

### 📖 Content

Every single front-end web test, no matter how complex, is made up of three simple, repeatable steps. We call this the **"Find, Act, Assert"** pattern.

1.  **Find** an element on the page (a button, an input field, some text). This is called using a **Selector**.
2.  **Act** on that element (click it, type into it, etc.). This is an **Action**.
3.  **Assert** that the page changed in the way you expected. This is an **Assertion**.

Let's break down each part using the elements on `https://demoqa.com/`.

#### 1. Selectors: How to *Find* an Element

A selector is an address you give the testing tool to find a unique element on the page. Here are the most common ways to do it:

*   **By ID:** The best and most stable way. An `id` should be unique on a page. Look for `id="..."` in the HTML. The selector is `#the-id`.
*   **By Class:** Finds elements with a specific CSS class. Look for `class="..."`. The selector is `.the-class-name`.
*   **By Text:** Finds an element that contains specific visible text. Very useful for buttons and links.

**Example:** Let's find the "Full Name" input field on the "Text Box" page (`https://demoqa.com/text-box`). In the HTML, it looks like this: `<input type="text" id="userName" ...>`. The `id` is `userName`.

---
##### <tabs>
<tab label="Playwright">
```javascript
// Find the element with the ID 'userName'
const fullNameInput = page.locator('#userName');
```
</tab>
<tab label="Cypress">
```javascript
// Find the element with the ID 'userName'
const fullNameInput = cy.get('#userName');
```
</tab>
<tab label="Selenium">```javascript
// Find the element with the ID 'userName'
const fullNameInput = await driver.findElement(By.id('userName'));
```</tab>
</tabs>

---

#### 2. Actions: How to *Interact* with an Element

Once you've found an element, you can perform actions on it. The two most common are:

*   `.type()` or `.sendKeys()`: To type text into an input field.
*   `.click()`: To click a button, link, or checkbox.

**Example:** Let's type a name into the "Full Name" field we just found.

---
##### <tabs>
<tab label="Playwright">
```javascript
const fullNameInput = page.locator('#userName');
// Type 'John Doe' into the field
await fullNameInput.type('John Doe');
```
</tab>
<tab label="Cypress">
```javascript
const fullNameInput = cy.get('#userName');
// Type 'John Doe' into the field
fullNameInput.type('John Doe');
```
</tab>
<tab label="Selenium">
```javascript
const fullNameInput = await driver.findElement(By.id('userName'));
// Type 'John Doe' into the field
await fullNameInput.sendKeys('John Doe');```
</tab>
</tabs>

---

#### 3. Assertions: How to *Check* the Result

This is the most important step! An automation script without an assertion is not a test—it's just a robot clicking around. An assertion is a check that either passes or fails.

Common assertions include:
*   Is the element visible?
*   Does the element contain specific text?
*   Does the element have a certain value?

**Example:** After submitting the form, a new piece of text appears showing our name. Let's assert that this output text is visible and correct. The HTML is `<p id="name">Name:John Doe</p>`.

---
##### <tabs>
<tab label="Playwright">```javascript
// Find the output element
const nameOutput = page.locator('#name');
// Assert that it is visible and contains the correct text
await expect(nameOutput).toBeVisible();
await expect(nameOutput).toHaveText('Name:John Doe');
```
</tab>
<tab label="Cypress">
```javascript
// Find the output element and chain assertions
cy.get('#name')
  .should('be.visible')
  .and('have.text', 'Name:John Doe');
```
</tab>
<tab label="Selenium">```javascript
// Find the output element
const nameOutput = await driver.findElement(By.id('name'));
// Assert it is visible
assert(await nameOutput.isDisplayed());
// Assert its text is correct
const text = await nameOutput.getText();
assert.equal(text, 'Name:John Doe');
```
</tab>
</tabs>

---

Master these three building blocks, and you can test almost any user interaction on the web.
