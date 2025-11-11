# Module 5: Handling the "Real" Web (Waits)

!!! warning
    AI generated content, no human review yet

### 🎯 Objective

In this module, you will learn why automated tests can be "flaky" and, more importantly, how to write stable and reliable tests by correctly handling waits. We will use dynamic elements on `demoqa.com` to clearly illustrate both the problem and its solution.

### 📝 Lesson Plan

| Topic | Description | Duration |
| :--- | :--- | :--- |
| **Why Tests Fail: The Web is Asynchronous** | Explain that code runs faster than websites load. Introduce the concept of "flaky" tests. | 20 mins |
| **Live Demo of the Problem** | Use the "Dynamic Properties" or "Progress Bar" page to show a test failing because an element isn't ready. | 20 mins |
| **The Solution: Implicit and Explicit Waits** | Explain that modern tools have "auto-waits" built-in. Demonstrate when and how to use an explicit wait for special cases. | 30 mins |
| **Lab: Make it Stable** | Students are given a flaky test for the "Progress Bar" page and must fix it by adding a proper wait. | 40 mins |
| **Q&A** | Discussion on strategies for dealing with dynamic content. | 10 mins |

### 📖 Content

#### Why Tests Can Be Unreliable (or "Flaky")

You will soon encounter a test that passes sometimes and fails other times for no apparent reason. This is a "flaky" test, and the #1 cause is **timing**.

Your test script can run in milliseconds. A website, however, needs time to load data, run animations, or enable a button. Your script might try to click a button that hasn't appeared on the screen yet, causing the test to fail.

**The Golden Rule:** Never assume the website will be ready. **Always wait.**

#### The Solution: Smart Waiting

Luckily, modern tools like Playwright and Cypress are designed to handle this for you most of the time. This is called an **implicit wait** or **auto-wait**.

When you write `page.locator('#myButton').click()`, the tool will automatically:
1.  Look for the button.
2.  If it's not there, it will wait for a few seconds.
3.  It will keep trying until the button appears or a timeout is reached (e.g., 5 seconds).
4.  Only *then* will it try to click.

This solves 90% of timing issues!

#### When Auto-Waits Aren't Enough: Explicit Waits

Sometimes, you need to wait for a specific condition that the tool doesn't know about. For example, on the `https://demoqa.com/dynamic-properties` page, a button is disabled for 5 seconds and then becomes enabled. An auto-wait might find the button, but it will fail when it tries to click the disabled button.

In this case, we need an **explicit wait**. We are explicitly telling the test: "Wait until this specific condition is met."

**Example:** Wait for the "Visible After 5 Seconds" button to appear and then click it.

---
##### <tabs>
<tab label="Playwright">
```javascript
// Playwright's locator actions auto-wait, so this is simple.
// It will wait for up to the timeout for the button to become visible.
const visibleButton = page.locator('#visibleAfter');
await visibleButton.click(); // This line implicitly waits for the button to be visible.

// For more complex conditions, you can use web-first assertions.
const colorChangeButton = page.locator('#colorChange');
// This will wait until the button's CSS 'color' property becomes red.
await expect(colorChangeButton).toHaveCSS('color', 'rgb(220, 53, 69)');
```
</tab>
<tab label="Cypress">```javascript
// Cypress commands also auto-wait.
// This will wait for up to the configured timeout for the button to exist and be clickable.
cy.get('#visibleAfter').click();

// You can also add explicit timeouts.
// Wait up to 10 seconds for this button to appear.
cy.get('#enableAfter', { timeout: 10000 }).should('be.enabled');
```</tab>
<tab label="Selenium">
```javascript
// Selenium requires more explicit waiting.
const visibleButton = await driver.wait(
  until.elementIsVisible(driver.findElement(By.id('visibleAfter'))),
  10000 // Timeout in milliseconds (10 seconds)
);
await visibleButton.click();
```
</tab>
</tabs>

---

Learning to use waits effectively is the difference between a flaky, unreliable test suite and a stable, trustworthy one.
