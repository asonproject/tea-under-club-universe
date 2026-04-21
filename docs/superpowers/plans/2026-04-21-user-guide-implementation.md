# Implementation Plan for User Guide Modal

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add a "?" help icon button that opens a user guide modal, explaining the tool's usage in simple terms for junior high school students.

**Architecture:** A new button will be added to the header. Clicking it will toggle the visibility of an existing modal (or a newly styled one), pre-filled with the user guide content.

**Tech Stack:** JavaScript, HTML, CSS.

---

### Task 1: Add Help Button to Header

**Files:**
- Modify: `tools/nenkan_keikaku.html`

- [ ] **Step 1: Add a new button element to the header HTML.**
    - Position it in the header, likely using CSS to align it to the top-right.
    - Use a "?" icon.

- [ ] **Step 2: Add a JavaScript event listener to the button.**
    - This listener will trigger the display of the help modal.

- [ ] **Step 3: Commit changes.**
    ```bash
    git add tools/nenkan_keikaku.html
    git commit -m "feat: add help button to header"
    ```

### Task 2: Style the Help Button and Modal

**Files:**
- Modify: `tools/nenkan_keikaku.html` (for CSS)

- [ ] **Step 1: Add CSS for the help button.**
    - Style it to be a small, circular button.
    - Use a font that matches the existing theme (e.g., "Zen Kurenaido").

- [ ] **Step 2: Add CSS for the help modal.**
    - Ensure it's visually appealing and matches the "notebook" or "memo" style described in the design.
    - Ensure it's responsive.

- [ ] **Step 3: Commit changes.**
    ```bash
    git add tools/nenkan_keikaku.html
    git commit -m "style: style help button and user guide modal"
    ```

### Task 3: Implement Help Modal Content and Logic

**Files:**
- Modify: `tools/nenkan_keikaku.html` (for JavaScript and HTML structure)

- [ ] **Step 1: Add the help guide text to the JavaScript `data` object or directly into the HTML structure.**
    - Use the drafted content from the design document, ensuring it's friendly and clear for junior high students.

- [ ] **Step 2: Implement the modal display logic.**
    - When the help button is clicked, show the modal.
    - Ensure the modal can be closed via the "X" button or by clicking outside.

- [ ] **Step 3: Commit changes.**
    ```bash
    git add tools/nenkan_keikaku.html
    git commit -m "feat: implement user guide modal content and display logic"
    ```

### Task 4: Verify Functionality and Accessibility

**Files:**
- N/A (Manual Verification)

- [ ] **Step 1: Manually test the "?" button.**
    - Click the button.
    - Verify the modal opens.
    - Verify the content is displayed correctly.
    - Verify the modal can be closed.

- [ ] **Step 2: Check responsiveness.**
    - Ensure the button and modal display correctly on different screen sizes.

- [ ] **Step 3: Commit changes (if any minor adjustments were made).**
    ```bash
    git add tools/nenkan_keikaku.html
    git commit -m "refactor: minor adjustments based on manual verification"
    ```
