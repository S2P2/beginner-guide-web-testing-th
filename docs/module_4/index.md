# Module 4: Writing Your First Full Test

### 🎯 Objective

In this module, you will combine the building blocks from Module 3 to write your first complete, structured test. You will learn the "Arrange, Act, Assert" pattern as a formal structure for creating clean and understandable tests.

###  📝 Lesson Plan

| Topic | Description | Duration |
| :--- | :--- | :--- |
| **Structuring Tests** | Introduce the "Arrange, Act, Assert" (AAA) pattern. Explain what each section is for. | 20 mins |
| **Live Demo: The Text Box Form**| Instructor codes a full test from scratch for `demoqa.com/text-box` using AAA, explaining each step. | 30 mins |
| **Lab: Your First Full Test** | **(Critical Lab)** Students are tasked to write their own test for the "Check Box" page (`demoqa.com/checkbox`). | 50 mins |
| **Code Review & Q&A** | Instructor reviews a few student solutions, highlighting good practices. | 20 mins |

### 📖 Content

#### Structure is Everything: Arrange, Act, Assert

Now that we have our building blocks, we need a blueprint to put them together. The most common and effective pattern for structuring a test is **Arrange, Act, Assert (AAA)**.

*   **Arrange:** Set up the test conditions. This is where you navigate to the webpage and prepare anything the test needs before the main interaction.

*   **Act:** Perform the key user action. This should ideally be a single, focused action, like "clicking the submit button" or "filling out the form."

*   **Assert:** Verify the outcome. This is where you check that the `Act` step resulted in the correct change on the webpage.

Using this pattern makes your tests easy to read, understand, and maintain.

#### Example: Testing the "Text Box" Form

Let's write a complete test for the form at `https://demoqa.com/text-box`.

**User Story:** A user should be able to fill out the text box form and see their submitted data displayed correctly.

---
##### <tabs>
<tab label="Playwright">
```javascript
import { test, expect } from '@playwright/test';

test('should successfully submit the text box form', async ({ page }) => {
  // Arrange: Navigate to the page
  await page.goto('https://demoqa.com/text-box');

  const fullNameInput = page.locator('#userName');
  const emailInput = page.locator('#userEmail');
  const submitButton = page.locator('#submit');

  // Act: Fill the form and click submit
  await fullNameInput.type('John Doe');
  await emailInput.type('john.doe@example.com');
  await submitButton.click();

  // Assert: Verify the output is visible and correct
  const nameOutput = page.locator('#name');
  const emailOutput = page.locator('#email');

  await expect(nameOutput).toBeVisible();
  await expect(emailOutput).toBeVisible();
  await expect(nameOutput).toHaveText('Name:John Doe');
  await expect(emailOutput).toHaveText('Email:john.doe@example.com');
});
```
</tab>
<tab label="Cypress">
```javascript
describe('Text Box Form', () => {
  it('should successfully submit the form', () => {
    // Arrange: Visit the page
    cy.visit('https://demoqa.com/text-box');

    // Act: Fill the form and click submit
    cy.get('#userName').type('John Doe');
    cy.get('#userEmail').type('john.doe@example.com');
    cy.get('#submit').click();

    // Assert: Verify the output is visible and correct
    cy.get('#name').should('be.visible').and('contain', 'John Doe');
    cy.get('#email').should('be.visible').and('contain', 'john.doe@example.com');
  });
});
```
</tab>
<tab label="Selenium">
```javascript
const { Builder, By, until } = require('selenium-webdriver');
const assert = require('assert');

describe('Text Box Form', function () {
  let driver;

  before(async function () {
    driver = await new Builder().forBrowser('chrome').build();
  });

  it('should successfully submit the form', async function () {
    // Arrange: Navigate to the page
    await driver.get('https://demoqa.com/text-box');

    // Act: Fill the form and click submit
    await driver.findElement(By.id('userName')).sendKeys('John Doe');
    await driver.findElement(By.id('userEmail')).sendKeys('john.doe@example.com');
    await driver.findElement(By.id('submit')).click();

    // Assert: Verify the output is visible and correct
    const nameOutput = await driver.findElement(By.id('name'));
    const emailOutput = await driver.findElement(By.id('email'));

    assert(await nameOutput.isDisplayed());
    assert.strictEqual(await nameOutput.getText(), 'Name:John Doe');
    assert.strictEqual(await emailOutput.getText(), 'Email:john.doe@example.com');
  });

  after(async () => await driver.quit());
});
```</tab>
</tabs>

---

Notice how each section of the test has a clear purpose. This makes it incredibly easy for anyone on your team to understand what the test is supposed to be doing.
