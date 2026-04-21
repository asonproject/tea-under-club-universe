# Design Document: User Guide Modal for Nenkan Keikaku

## 1. Overview
Add a user guide button (icon) to the top-right corner of the application. When clicked, it opens a modal window explaining how to use the "Nenkan Keikaku" tool in simple terms suitable for junior high school students.

## 2. Requirements
- **Help Button**: A "?" icon button positioned at the top-right of the header.
- **Guide Modal**: A visually appealing modal window showing the guide content.
- **Simple Content**: Clear, 3-step instructions using friendly language.
- **Close Action**: Easy way to close the guide (X button or clicking outside).

## 3. Implementation Details

### 3.1 UI Components
- **Button**: 
    - Position: `absolute` or `fixed` at the top-right of the header/screen.
    - Style: Circular button with a "?" icon, matching the "Kaisei Decol" and "Zen Kurenaido" fonts.
- **Modal**:
    - Re-use the existing `modal-overlay` and `modal` structure or create a dedicated `help-modal`.
    - Style: Friendly "notebook" or "memo" look with clean spacing.

### 3.2 Guide Content (Draft)
**タイトル: 年間計画表の使い方**
1. **自由に書こう！**
    - 表の中の「白っぽい部分」をタップすると、好きな言葉を入力できるよ！
    - 「(未記入)」と書いてあるところも、タップすればすぐに書き直せるから安心。
2. **ボタンで切り替え！**
    - 「年」「半期」「四半期」「月」「週」のボタンを押すと、表示が切り替わるよ。
    - 1年間の大きな目標から、1週間の小さな予定まで、好きなスケールで考えてみよう！
3. **保存して印刷しよう！**
    - 「保存」ボタンを押すと、入力した内容がブラウザに記録されるよ。
    - 「印刷」ボタンを押すと、自分だけの計画表がカッコよくプリントできちゃう！
    - 「MD出力」を使えば、テキストとして保存して他のアプリで使うこともできるよ。

## 4. Verification Plan
- **Manual Check**: Click the "?" button and verify the modal opens correctly.
- **Content Review**: Ensure the text is readable and correctly reflects the tool's features.
- **Responsiveness**: Check the button and modal layout on both desktop and mobile views.
