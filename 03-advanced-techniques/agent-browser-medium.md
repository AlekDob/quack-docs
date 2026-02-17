This guide shows you how to use agent-browser to publish article drafts directly to Medium from Quack agents.

## Overview

The `medium-writer` skill automates the process of publishing text content to Medium as a draft. After an agent writes an article (typically saved in your Obsidian vault), it can push the content to Medium for review and final publishing.

> **Note:** Agent Browser publishes drafts only. You'll review, add images, and publish manually via Medium's interface.

## Prerequisites

Before publishing to Medium, ensure:

1. **agent-browser is installed**: `npm install -g agent-browser`
2. **Chrome is running with CDP**: See [Setup Guide](./agent-browser-setup#cdp-setup-for-cloudflare-protected-sites)
3. **You're logged into Medium** in that Chrome instance
4. **Article is written and ready** (e.g., in Obsidian or a text file)

## Pre-Flight Check

Always verify CDP connection before publishing:

```bash
curl -s http://localhost:9222/json/version
```

If this fails, Chrome is not running with debugging. Follow these steps:

1. Close Chrome completely (`Cmd+Q` on macOS)
2. Reopen with debugging:
   ```bash
   /Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome \
     --remote-debugging-port=9222 \
     --user-data-dir=/tmp/chrome-debug
   ```
3. Log into Medium manually (Google or email login)

## Publishing Workflow

### Step 1: Open New Story Page

Navigate to Medium's new story editor:

```bash
agent-browser --cdp 9222 open https://medium.com/new-story
```

Wait for the page to load. You should see the Medium editor with "Tell your story..." placeholder.

### Step 2: Insert the Title

Medium's title is an `<h3>` element with `data-testid="editorTitleParagraph"`. Use JavaScript to select and replace it:

```bash
agent-browser --cdp 9222 eval "
const h3 = document.querySelector('h3[data-testid=\"editorTitleParagraph\"]');
h3.click();
h3.focus();
const range = document.createRange();
range.selectNodeContents(h3);
const sel = window.getSelection();
sel.removeAllRanges();
sel.addRange(range);
document.execCommand('insertText', false, 'Your Article Title Here');
"
```

Replace `'Your Article Title Here'` with the actual title.

> **Warning:** Never use the `fill` or `type` commands on Medium's editor. They cause "Something is wrong" save errors. Always use `eval` with `document.execCommand('insertText')`.

### Step 3: Insert Body Paragraphs

Press Enter to move to the body, then insert text one paragraph at a time:

```bash
# Move to body
agent-browser --cdp 9222 press Enter

# Insert first paragraph
agent-browser --cdp 9222 eval "document.execCommand('insertText', false, 'First paragraph text here.')"

# New paragraph
agent-browser --cdp 9222 press Enter
agent-browser --cdp 9222 eval "document.execCommand('insertText', false, 'Second paragraph text here.')"
```

Repeat for each paragraph. Each `press Enter` creates a new paragraph block.

### Step 4: Insert Subheadings

For subheadings, insert text with Markdown syntax:

```bash
agent-browser --cdp 9222 press Enter
agent-browser --cdp 9222 eval "document.execCommand('insertText', false, '## Subheading Here')"
agent-browser --cdp 9222 press Enter
```

Medium will auto-convert `##` to a formatted heading.

For larger headings, use `#` (h2) or `###` (h4).

### Step 5: Insert Italic Text (Author Bio)

For the author bio at the end, insert the text then manually format it:

```bash
agent-browser --cdp 9222 press Enter
agent-browser --cdp 9222 press Enter
agent-browser --cdp 9222 eval "document.execCommand('insertText', false, 'I am Alek, an AI-first developer building things from Puglia, Italy. Currently working on Quack...')"
```

Then select the text and press `Cmd+I` (macOS) or `Ctrl+I` (Windows) to italicize.

> **Note:** Inline formatting (bold, italic, links) is easier to add manually during review. Agent Browser can insert plain text, and you can format it in Medium's editor before publishing.

### Step 6: Verify and Save

Medium auto-saves drafts. Verify the save status:

```bash
agent-browser --cdp 9222 snapshot | head -25
```

Look for `text: DraftSaved` or similar confirmation in the output.

If you see "Something is wrong and we cannot save your story", the insertion method may have triggered an error. Close the tab and start fresh.

### Step 7: Get Draft URL

After saving, get the draft URL:

```bash
agent-browser --cdp 9222 get url
```

Copy this URL and share it with the user for review.

## The execCommand Trick

Medium (like Notion and other rich text editors) uses `contenteditable` divs instead of standard `<input>` or `<textarea>` elements. Playwright's `fill` and `type` commands don't work correctly with these editors.

The solution: `document.execCommand('insertText', false, 'text')`

This JavaScript API simulates typing and works with contenteditable elements. It's how Medium's own UI inserts text when you type.

**Rule**: Always use `eval` with `execCommand` for Medium text insertion.

## Limitations

### No Image Uploads

Agent Browser cannot upload images to Medium yet. Publish the draft as text-only, then add images manually during review.

To add images:
1. Open the draft URL in your browser
2. Click the `+` button in the left margin
3. Select "Image" and upload

### No Code Blocks

Code blocks require special formatting in Medium. You can:

- Type triple backticks (\`\`\`) and Medium will create a code block
- Click the `<>` icon in the Medium editor
- Or add code blocks during manual review

### No Automatic Publishing

Agent Browser only creates drafts. You must:
1. Review the draft for formatting and accuracy
2. Add images, code blocks, and other media
3. Click "Publish" manually in Medium's interface
4. Set tags, subtitle, and publication (if applicable)

This is intentional — automated publishing without review can lead to formatting issues or incomplete content.

## Full Example

Here's a complete workflow to publish a simple article:

```bash
# 1. Pre-flight check
curl -s http://localhost:9222/json/version

# 2. Open new story
agent-browser --cdp 9222 open https://medium.com/new-story

# 3. Insert title
agent-browser --cdp 9222 eval "
const h3 = document.querySelector('h3[data-testid=\"editorTitleParagraph\"]');
h3.click(); h3.focus();
const range = document.createRange();
range.selectNodeContents(h3);
const sel = window.getSelection();
sel.removeAllRanges(); sel.addRange(range);
document.execCommand('insertText', false, 'I Stopped Using One Claude Code Session. I Now Ship 3x Faster.');
"

# 4. Insert first paragraph
agent-browser --cdp 9222 press Enter
agent-browser --cdp 9222 eval "document.execCommand('insertText', false, 'Every Claude Code user knows this feeling. You type a request. Claude starts working. And then you wait.')"

# 5. Insert second paragraph
agent-browser --cdp 9222 press Enter
agent-browser --cdp 9222 eval "document.execCommand('insertText', false, 'For months, I ran a single Claude Code session at a time. One task, one terminal, one long wait.')"

# 6. Insert subheading
agent-browser --cdp 9222 press Enter
agent-browser --cdp 9222 press Enter
agent-browser --cdp 9222 eval "document.execCommand('insertText', false, '## The Problem')"
agent-browser --cdp 9222 press Enter

# 7. More content...
agent-browser --cdp 9222 eval "document.execCommand('insertText', false, 'The single-session workflow creates artificial bottlenecks.')"

# 8. Verify save
agent-browser --cdp 9222 snapshot | grep -i "draft"

# 9. Get URL
agent-browser --cdp 9222 get url
```

## Post-Publishing Workflow

After the draft is created:

1. **Review in Medium**: Open the draft URL and check formatting
2. **Add media**: Upload images, embed videos, add code blocks
3. **Set metadata**: Add tags, subtitle, and choose publication (if applicable)
4. **Publish**: Click "Publish" and set visibility (Public, Unlisted, etc.)
5. **Update Obsidian**: Change article status from `draft` to `published`, add Medium URL

## Troubleshooting

### "Something is wrong" Error

This happens when using `fill` or `type` commands. Always use `eval` with `execCommand`.

If you see this error after using `execCommand`, the page may be corrupted. Close the tab and start fresh:

```bash
agent-browser --cdp 9222 close
agent-browser --cdp 9222 open https://medium.com/new-story
```

### Cloudflare Block

If Medium shows a Cloudflare challenge page:

- Verify you're using `--cdp 9222` flag
- Check that Chrome is running with debugging (`lsof -i :9222`)
- Make sure you're logged into Medium in that Chrome instance
- Complete any Cloudflare challenges manually in the Chrome window

### Text Not Appearing

If text doesn't appear after `execCommand`:

- Take a snapshot to see the current page state
- Verify the title was inserted correctly (it's the entry point)
- Try pressing Enter before inserting text
- Check if Medium's editor is focused (click it manually if needed)

### Draft Not Saving

Medium auto-saves every few seconds. If you don't see "DraftSaved" in the snapshot:

- Wait 5-10 seconds and snapshot again
- Refresh the page to trigger a save
- Check browser console for JavaScript errors

## Next Steps

- [Medium Writer Skill](/.claude/skills/medium-writer) — Full writing guide with title formulas and article structure
- [Agent Browser Overview](./agent-browser-overview) — Learn about other automation use cases

---

**Previous**: [Agent Browser Setup](./agent-browser-setup)
**Next**: [Best Practices](../04-best-practices)
