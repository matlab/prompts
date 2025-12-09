# Contributing to Prompts for MATLAB

This guide explains how to add prompts to the collection.

## How to Contribute

1. **Fork the repository**
2. **Choose or create a category** in the `prompts/` directory
3. **Create your prompt file** using the [template](templates/prompt-template.md)
4. **Add your prompt to the category README**
5. **Submit a pull request**

## Prompt Guidelines

### Quality Standards

Your prompt should be:
- **Tested:** Verify it works with at least one AI coding assistant
- **Clear:** Easy to understand and use
- **Complete:** Include all necessary context and requirements
- **Practical:** Solve a real problem MATLAB users face
- **Well-documented:** Include usage examples and tips

### What Makes a Good Prompt?

**Good prompts:**
- Specify concrete requirements
- Include example inputs/outputs
- Mention MATLAB release requirements
- List required toolboxes
- Provide usage examples
- Explain expected results

**Avoid:**
- Vague or ambiguous requests
- Overly complex multi-step prompts (break them down)
- Prompts requiring specific proprietary data
- Duplicates of existing prompts

## File Structure

### Prompt File Template

Each prompt should be a markdown file with this structure:

```markdown
---
title: Prompt Title
description: One-line description
tags: [matlab, relevant, tags]
release: R2024a+ or "All releases" or "Requires ToolboxName"
notes: 
---

# Prompt Title

Brief description (1-2 sentences).

## Metadata

- **Tags:** List with backticks
- **MATLAB Release:** Requirements
- **Required Toolboxes:** List or "None"
- **Difficulty:** Level

## The Prompt

\`\`\`text
Your actual prompt text here.
Include all instructions and placeholders like [PASTE CODE HERE].
\`\`\`

## Usage Tips

1. Tip one
2. Tip two
3. Tip three

## Example Usage

### Example 1: Descriptive Name

\`\`\`
Example of using the prompt with specific values filled in
\`\`\`

## Related Prompts

- [Related Prompt 1](../category/prompt-name.md)
- [Related Prompt 2](other-prompt.md)

## References

- [MATLAB Documentation Link](https://www.mathworks.com/help/...)
```

### Category README

After adding your prompt file, update the category's README.md:

```markdown
### [Your Prompt Name](your-prompt-file.md)
Brief one-line description of what the prompt does.

**Tags:** `tag1` `tag2` `tag3`
**Release:** Requirements
```

## Categories

Choose the most appropriate category for your prompt:

- **live-scripts-documentation** - Live Scripts, documentation, help text
- **programming** - Core MATLAB, performance, error handling, testing
- **ai-and-statistics** - ML, deep learning, statistics
- **signal-processing** - DSP, filters, spectral analysis
- **image-processing-and-computer-vision** - Computer vision, image enhancement
- **control-systems** - Controllers, stability, system modeling
- **code-generation** - MATLAB Coder, deployment, compilation

If your prompt doesn't fit any category, propose a new one in your pull request.

## Naming Conventions

### File Names
- Use lowercase with hyphens: `my-prompt-name.md`
- Be descriptive: `design-digital-filter.md` not `filter.md`
- Avoid version numbers in names

### Prompt Titles
- Use title case: "Design Digital Filter"
- Be specific: "Build Neural Network with Deep Learning Toolbox" not "Create Network"
- Start with action verbs: Design, Create, Analyze, Optimize, etc.

## Tags

Use consistent, searchable tags:

### Toolbox Tags
Use official toolbox names:
- `signal-processing-toolbox`
- `image-processing-toolbox`
- `deep-learning-toolbox`
- `statistics-and-machine-learning-toolbox`
- `control-system-toolbox`

### Feature Tags
Common tags to use:
- `matlab` (always include)
- `optimization`, `vectorization`, `performance`
- `error-handling`, `validation`, `testing`
- `classification`, `regression`, `clustering`
- `filter-design`, `fft`, `spectral-analysis`
- `live-script`, `documentation`
- `deployment`, `code-generation`

### Release Tags
- `r2024a`, `r2025a`, etc. (when specific features from that release are required)

## Release Requirements

Be specific about MATLAB release requirements:

- **"All releases"** - Works with any MATLAB version
- **"R2019b+"** - Requires R2019b or newer (e.g., for arguments block)
- **"R2025a+"** - Requires specific release features
- **"Requires Toolbox Name"** - Specify toolbox requirements

## Testing Your Prompt

Before submitting, test your prompt:

1. **Try it yourself** with an AI coding assistant
2. **Verify the output** meets the prompt requirements
3. **Test with variations** to ensure robustness
4. **Check for edge cases** mentioned in the prompt

## Pull Request Process

1. **Fork and create a branch** (`git checkout -b add-new-prompt`)
2. **Add your prompt file** to the appropriate category folder
3. **Update the category README** with your prompt
4. **DO NOT update the main README** (stays static)
5. **Commit with clear message** (`git commit -m "Add prompt for X"`)
6. **Push and create PR** with description of your prompt

### PR Description Template

```markdown
## Prompt: [Prompt Name]

**Category:** [category-name]
**Tested with:** [AI tool names]

### What does this prompt do?
[Brief description]

### Why is it useful?
[Explain the use case]

### Testing
- [ ] Tested with at least one AI coding assistant
- [ ] Includes usage examples
- [ ] Added to category README
- [ ] Follows template structure
```

## Code of Conduct

- Be respectful and constructive
- Focus on quality over quantity
- Help improve existing prompts
- Credit others' work when building on it

## Questions?

- Open an issue for questions or suggestions
- Check existing prompts for examples
- Review the [prompt template](templates/prompt-template.md)

## License

By contributing, you agree to license your contributions under the CC-BY-4.0 license.

---

We appreciate your contributions.
