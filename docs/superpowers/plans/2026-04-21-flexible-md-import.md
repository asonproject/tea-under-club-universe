# Flexible MD Import Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Update the "Nenkan Keikaku" tool to flexibly import MD files with bold markers (`**`) and update the export format for the "Last updated" line.

**Architecture:** Modify the `fromMarkdown` and `toMarkdown` JavaScript functions within `tools/nenkan_keikaku.html` using more robust regular expressions and string cleaning.

**Tech Stack:** JavaScript (Vanilla), HTML, CSS.

---

### Task 1: Update Export Format (toMarkdown)

**Files:**
- Modify: `tools/nenkan_keikaku.html`

- [ ] **Step 1: Modify `toMarkdown` to use triple asterisks for the "Last updated" line.**

```javascript
// Change this line:
md += `---\n\n*Last updated: ${new Date().toISOString().slice(0, 10)}*\n`;
// To this:
md += `---\n\n***Last updated: ${new Date().toISOString().slice(0, 10)}***\n`;
```

- [ ] **Step 2: Verify export output**
Open the tool, enter some data, click "MD出力" and verify the last line is `***Last updated: YYYY-MM-DD***`.

- [ ] **Step 3: Commit changes**

```bash
git add tools/nenkan_keikaku.html
git commit -m "feat: update MD export date format to triple asterisks"
```

### Task 2: Update Title and Header Parsing (fromMarkdown)

**Files:**
- Modify: `tools/nenkan_keikaku.html`

- [ ] **Step 1: Update Title/Subtitle extraction to strip bold markers.**

```javascript
// Existing:
const titleMatch = line.match(/^#\s+(.+)$/);
if (titleMatch && !result.title) {
  result.title = titleMatch[1].trim();
  continue;
}
// Proposed:
const titleMatch = line.match(/^#\s+(.+)$/);
if (titleMatch && !result.title) {
  result.title = titleMatch[1].trim().replace(/^(\*\*|__)(.*)(\*\*|__)$/, '$2');
  continue;
}
// Similar for subMatch
```

- [ ] **Step 2: Update section header regex to allow optional bolding.**

```javascript
// Update regex for:
// - /^##\s+年間計画/
// - /^##\s+上半期/
// - /^##\s+下半期/
// - /^###\s+Q(\d)/
// - /^###\s+(\d+)月/
// to handle optional ** around the labels.
```

- [ ] **Step 3: Run: Import a file with bolded headers to verify.**
Example line: `## **年間計画**`
Expected: Section `year` is correctly identified.

- [ ] **Step 4: Commit changes**

```bash
git add tools/nenkan_keikaku.html
git commit -m "feat: support bold markers in MD headers during import"
```

### Task 3: Update Weekly Item Parsing (fromMarkdown)

**Files:**
- Modify: `tools/nenkan_keikaku.html`

- [ ] **Step 1: Improve weekly item extraction regex in `fromMarkdown`.**

```javascript
// Current:
const wm = l.match(/^-\s*\*\*W(\d)\*\*:\s*(.*)$/);
// Proposed (handles multiple bolding styles):
const wm = l.match(/^-\s*(\*\*|)W(\d)(:|\*\*|: \*\*|)\s*(.*?)(\*\*|)$/);
// Logic:
// 1. Match optional ** before W
// 2. Capture W digit
// 3. Match separator (:, **, or : **)
// 4. Capture content
// 5. Match optional ** at the end
```

- [ ] **Step 2: Update cleaning logic for content.**
Ensure `(未記入)` and `**(未記入)**` are treated as empty.

- [ ] **Step 3: Verify with user's specific examples.**
Import: `- **W2: 6/14,15 人権講話＠泊高校**`
Expected: `6/14,15 人権講話＠泊高校` is extracted for W2.

- [ ] **Step 4: Commit changes**

```bash
git add tools/nenkan_keikaku.html
git commit -m "feat: robust weekly item parsing for MD import"
```
