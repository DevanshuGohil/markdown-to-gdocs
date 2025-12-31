# Markdown to Google Docs Converter

A Python script for Google Colab that converts markdown meeting notes into a well-formatted Google Doc with proper headings, bullet points, checkboxes, and styled @mentions.

## Features

- **Heading Conversion**: H1, H2, H3 markdown headings → Google Docs Heading 1, 2, 3 styles
- **Bullet Point Hierarchy**: Nested bullet points with proper indentation
- **Checkbox Support**: Converts `- [ ]` markdown checkboxes to Google Docs checkboxes
- **@Mention Styling**: @mentions are displayed in bold blue text
- **Footer Styling**: Meeting metadata displayed in italic gray text
- **Error Handling**: Comprehensive try-catch blocks with helpful error messages

## Prerequisites

- Google Account
- Access to Google Colab
- Google Docs API enabled (automatic in Colab)

## Required Dependencies

The following packages are installed automatically in the notebook:

```
google-api-python-client
google-auth-httplib2
google-auth-oauthlib
```

## Setup Instructions

### Option 1: Run Directly in Google Colab

1. Open Google Colab: [colab.research.google.com](https://colab.research.google.com)
2. Click **File → Upload notebook**
3. Upload the `markdown_to_gdoc.ipynb` file
4. Run each cell in order (Shift + Enter)

### Option 2: Open from GitHub

1. Open Google Colab
2. Click **File → Open notebook**
3. Select the **GitHub** tab
4. Enter the repository URL
5. Select `markdown_to_gdoc.ipynb`

## How to Run in Colab

1. **Run the installation cell** - Installs required Google API libraries

2. **Run the authentication cell** - A popup will appear asking you to:
   - Select your Google account
   - Grant permissions for Google Docs and Drive access
   - Click "Allow" to proceed

3. **Run the markdown content cell** - Loads the meeting notes

4. **Run the converter class cell** - Defines the conversion logic

5. **Run the final conversion cell** - Creates the Google Doc
   - A clickable link will appear to open your formatted document

## Project Structure

```
markdown-to-gdocs/
├── README.md                 # This file
├── markdown_to_gdoc.ipynb    # Main Colab notebook
└── sample_meeting_notes.md   # Sample markdown input (optional)
```

## Code Overview

### Main Components

| Component | Description |
|-----------|-------------|
| `MarkdownToGoogleDocsConverter` | Main class handling the conversion |
| `create_document()` | Creates a new Google Doc via API |
| `parse_markdown()` | Parses markdown and generates API requests |
| `apply_formatting()` | Executes batched formatting requests |

### Formatting Mapping

| Markdown | Google Docs Style |
|----------|-------------------|
| `# Title` | Heading 1 |
| `## Section` | Heading 2 |
| `### Subsection` | Heading 3 |
| `- Item` or `* Item` | Bullet point |
| `  - Nested` | Indented bullet |
| `- [ ] Task` | Checkbox |
| `@name` | Bold + Blue color |
| Footer text | Italic + Gray color |

## Customization

### Modifying Input Content

Replace the `MARKDOWN_CONTENT` variable with your own markdown:

```python
MARKDOWN_CONTENT = """# Your Meeting Title
## Your Section
- Your bullet points
"""
```

### Changing @Mention Styling

Modify the color in `_process_mentions()`:

```python
'rgbColor': {'red': 0.0, 'green': 0.4, 'blue': 0.8}  # Blue
```

### Adjusting Indentation

Change the indentation multiplier in `_add_bullet_point()`:

```python
'indentStart': {'magnitude': 36 * nesting_level, 'unit': 'PT'}
```

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Authentication fails | Re-run the auth cell and ensure popups aren't blocked |
| API quota exceeded | Wait a few minutes and try again |
| Document not created | Check Google account has Docs access |
| Formatting issues | Ensure markdown follows standard syntax |

## Example Output

The converter transforms this markdown:

```markdown
## Action Items
- [ ] @sarah: Finalize Q3 roadmap by Friday
```

Into a Google Doc with:
- "Action Items" as Heading 2
- A checkbox list item
- "@sarah" in bold blue text

## License

MIT License - Feel free to use and modify for your projects.

## Author

Created for Full Stack Software Engineer Assessment

---

**Note**: This tool requires an active internet connection and Google account authentication to function properly.
