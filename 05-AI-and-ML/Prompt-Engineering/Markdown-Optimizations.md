User: [dir](../frontend/src/types/api.ts:23) -- explain how do I specify the line in the directory path

GitHub Copilot: To specify a line number in a file path link in Markdown (which is supported by VS Code and platforms like GitHub), you should use the `#L` syntax followed by the line number, rather than a colon (`:`).

Here is how you should format your link:

**For a single line:**
```markdown
[dir](../frontend/src/types/api.ts#L23)
```

**For a range of lines:**
```markdown
[dir](../frontend/src/types/api.ts#L23-L30)
```

VS Code and GitHub will parse the `#L23` anchor and automatically scroll to line 23 when the link is clicked.






---

User: what does `L` means? Is there anything else?

GitHub Copilot: The `L` simply stands for **Line**. It is a standard URL fragment identifier convention used by Visual Studio Code, GitHub, GitLab, and Bitbucket to highlight or scroll to a specific line in a source code file.

Here is what else you can do with URL fragments (`#`) after a file path:

**1. Line Ranges**
You can specify a range of lines by connecting two `L` identifiers with a hyphen.
Format: `[description](path/to/file.ts#L10-L20)`
*This highlights everything from line 10 down to line 20.*

**2. Markdown Headings**
If you are linking to another Markdown (`.md`) file, you can link directly to a specific heading by omitting the `L` and using the heading name (lowercased, with spaces replaced by hyphens).
Format: `[description](path/to/readme.md#installation-instructions)`

**3. Diffs (GitHub Specific)**
When viewing pull requests or commits on GitHub, you might see `R` and `L` used in the URL fragments to denote the **Right** (new/added) and **Left** (old/removed) sides of a code diff.
Example: `#diff-filenameR25` (Right side, line 25). You generally do not write these manually, but it is another way letters are used in file paths.







User: How to embed image into the mark down file? Give an example for every source of image (from / assets folder or the internet)?

---

How do I adjust the width and position of that image?

GitHub Copilot: ## Embedding Images in Markdown

**Syntax:**
```markdown
![alt text](source)
```

---

### 1. From a Local assets Folder
```markdown
![My Image](./assets/image.png)
![My Image](../assets/image.png)
```

### 2. From the Internet (URL)
```markdown
![My Image](https://example.com/image.png)
```

---

## Adjusting Width & Position

Standard Markdown does **not** support width or alignment natively. You need to use an **HTML `<img>` tag** instead:

### Width
```html
<img src="./assets/image.png" alt="My Image" width="300">
```

### Position / Alignment

**Center:**
```html
<div align="center">
  <img src="./assets/image.png" alt="My Image" width="300">
</div>
```

**Left / Right:**
```html
<img src="./assets/image.png" alt="My Image" width="300" align="left">
<img src="./assets/image.png" alt="My Image" width="300" align="right">
```

> **Note:** HTML tags work in GitHub READMEs and most Markdown renderers, but may not work in strict Markdown-only environments.