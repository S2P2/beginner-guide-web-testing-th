# Module 2: Getting Your Tools Ready

!!! warning
    AI generated content, no human review yet

### 🎯 Objective

In this module, your objective is to overcome the first major hurdle: software installation and project setup. You will learn how to set up your development environment, familiarize yourself with our demo application, and get your project to a "ready to code" state.

### 📝 Lesson Plan

| Topic | Description | Duration |
| :--- | :--- | :--- |
| **Pre-requisites Check** | Ensure everyone has Node.js and a code editor (like VS Code) installed. | 15 mins |
| **Introducing Our Playground** | A guided tour of `https://demoqa.com/`. Explain why it's a perfect learning environment. | 15 mins |
| **Live Setup Demo** | Instructor walks through setting up a new project from scratch for **one** tool (e.g., Playwright). | 30 mins |
| **Lab: Your Turn!** | Students follow a step-by-step guide on the tutorial page to install their chosen framework(s). | 45 mins |
| **Q&A and Troubleshooting** | Help students who are stuck. | 15 mins |

### 📖 Content

#### The Pre-requisites

Before we can start, you need two things on your computer:
1.  **Node.js:** This is the underlying technology that lets us run JavaScript outside of a web browser. The testing tools we are using are built on it.
2.  **A Code Editor:** This is the program where you'll write your test scripts. We highly recommend **Visual Studio Code (VS Code)** as it's free, powerful, and has great support for these tools.

#### Our Playground: `https://demoqa.com/`

For this entire course, we will only use one website for all our examples and labs: **`https://demoqa.com/`**.

Why?
*   **It's Stable:** It was built specifically for people to practice automation on. It won't change unexpectedly and break our tests.
*   **It's Diverse:** It contains all the common web elements you will encounter in the real world: text boxes, check boxes, radio buttons, dynamic forms, progress bars, and more.
*   **It's Safe:** We can experiment and practice as much as we want without worrying about affecting a real application.

We will primarily be using the "Elements" section to start.

#### Setting Up Your First Project

This is the only part of the course that is truly framework-specific. Follow the instructions for the tool you want to start with. The process is very similar for all of them.

1.  Create a new folder on your computer (e.g., `my-first-tests`).
2.  Open that folder in your code editor (VS Code).
3.  Open the built-in terminal in your editor.

---
##### <tabs>
<tab label="Playwright">
Run this single command in your terminal. It will ask you a few questions—just accept the defaults by pressing `Enter`.
```bash
npm init playwright@latest
```
This command automatically:
*   Sets up your project.
*   Creates a `playwright.config.js` file for settings.
*   Creates an `e2e` folder with an example test file.
*   Installs the browsers you need (Chromium, Firefox, WebKit).

Your first blank test file will be in `tests/example.spec.js`.
</tab>
<tab label="Cypress">
Run this single command in your terminal:
```bash
npm install cypress --save-dev
```
Once it finishes, run this command to open Cypress for the first time:
```bash
npx cypress open
```
The Cypress app will launch and guide you through creating your first E2E (End-to-End) test. It will automatically create a `cypress` folder and a `cypress.config.js` file.

Your first blank test file will be in `cypress/e2e/`.
</tab>
<tab label="Selenium">
Selenium setup is slightly more manual. First, initialize your project by running:
```bash
npm init -y
```
This creates a `package.json` file. Now, install Selenium's library:
```bash
npm install selenium-webdriver
```You don't need to install browsers separately; Selenium will use the ones already on your machine (like Chrome or Firefox). You'll need to create a test file yourself (e.g., `test.js`).
</tab>
</tabs>

---

By the end of this module, you should have a project folder with a blank test file ready to go!
