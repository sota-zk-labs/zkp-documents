# DOCUMENTATION REPOSITORY

This repository serves as a comprehensive resource for Zero-Knowledge Proofs (ZKPs), covering theoretical aspects,
terminology, academic papers, and articles related to the subject.

## How To Use This Repository

### Prerequisite

[**Obsidian**](https://obsidian.md): While any markdown editor should be able to view/edit this repository, we recommend
using this app since predefined settings are included in the repo to simplify your experience.

### Common Guidelines

To maintain consistency in our repo content, please adhere to this checklist:

- [ ] File names should be written in snake_case format.
- [ ] Folder names should be written in dash-case format.
- [ ] Every markdown file must have a header.
- [ ] Every article should have its attributes defined.
- [ ] Any media files (images, PDFs, etc.) should be placed under the `attachments` folder in the current editing file.
- [ ] Ensure every article has at least the same number of headers as in the corresponding PDF file.

### Level

Each article will have a `level` attribute with the value ranging from 1 to 10, where 1 means easiest to read and 10
means hardest to read.

### Repository Structure

- **terms:** This directory provides an introduction to basic terminology essential for understanding ZKP concepts.

- **articles:** Explore this directory for PDFs of academic papers and articles related to ZKPs. Additionally, find
  details, comments, and reading status notes to aid comprehension.

- **docs:** This directory contains definitions, explanations, and documentation pertaining to various types of ZKPs and
  specific ZKP technologies.

- **english:** Don't know how to pronounce math formulas? View this folder.

- **presentations:** This directory contains all our presentation slides.

- **anki:** This directory contains flashcards used to memorize ZKP-related contents.

### How to create/sync Flashcards with Anki

1. Follow the instruction written in [here](https://github.com/reuseman/flashcards-obsidian) to connect with Anki.
2. Mark a header as flashcard by adding a hidden link `[]()` at the end of the header.
3. Run `Flashcard: Generate for the current file`.

### Markdown Linter

We use [markdownlint](https://github.com/DavidAnson/markdownlint/tree/main) to ensure consistency in our markdown files.
Please install the linter and run it before submitting a PR. You can find the configuration file in the root directory
of this repository.

To install the linter, run the following command:

```bash
npm install -g markdownlint-cli
```

If you want to run it manually, you can use the following command:

```bash
markdownlint '**/*.md' --fix
```

If you want to make the linter run automatically when you commit your changes:

```bash
cp pre-commit .git/hooks/
```

---
This structured organization aims to facilitate ease of navigation and comprehension for individuals seeking information
on Zero-Knowledge Proofs. Regular updates and contributions to expand the repository's content are highly encouraged
through the standard Pull Request (PR) process. Thank you for your commitment to building a valuable resource on ZKP.
