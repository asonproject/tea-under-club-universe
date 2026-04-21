# Design Document: Flexible MD Import for Nenkan Keikaku

## 1. Overview
Update `tools/nenkan_keikaku.html` to support a more flexible Markdown import format, specifically handling bold markers (`**`) around headers, sections, and list items. This allows users to import content exported from other editors or styled manually without breaking the tool's parser.

## 2. Requirements
- **Flexible Import**: `fromMarkdown` must recognize headers and weekly items even if they are wrapped in `**`.
- **Placeholder Handling**: Correctly ignore `**(未記入)**` as empty content.
- **Consistent Export**: `toMarkdown` should maintain its current clean output style (minimal bolding) but update the "Last updated" line to use triple asterisks (`***`).

## 3. Implementation Details

### 3.1 `fromMarkdown` Updates
- **Title/Subtitle**: Strip leading/trailing `**` and `__`.
- **Headers**:
    - Update regex for `## 年間計画`, `## 上半期`, etc., to allow optional bold markers.
    - Example: `/^##\s+(\*\*|)年間計画(\*\*|)/`
- **Sections (Q1, 4月 etc.)**:
    - Update regex to allow optional bold markers.
    - Example: `/^###\s+(\*\*|)(Q\d|\d+月)/`
- **Weekly Items**:
    - Support multiple formats:
        1. `- **W1**: content` (existing)
        2. `- **W1: content**` (user's new format)
        3. `- **W1:** content` (empty content with bold prefix)
        4. `- W1: content` (plain)
- **Cleaning**: Ensure `(未記入)` and `**(未記入)**` are treated as `""`.

### 3.2 `toMarkdown` Updates
- Change `*Last updated: ...*` to `***Last updated: ...***`.
- Maintain existing styles for sections and items to avoid unexpected changes to user's saved files.

## 4. Verification Plan
- **Test Case 1: Simple Import**: Import standard markdown and verify data is correctly populated.
- **Test Case 2: Bold Import**: Import the user-provided bolded markdown and verify all items (手術, 講話, etc.) are correctly mapped to their respective weeks.
- **Test Case 3: Export Integrity**: Export the data and verify the "Last updated" format is correct and titles/sections are clean.
