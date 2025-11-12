# GitHub Copilot Custom Instructions Template

Template for customizing GitHub Copilot commit message generation in VS Code using Conventional Commits standard.

## What's Included

- `copilot-commit-message-instructions.md` - Condensed guidelines for generating conventional commit messages

## Usage in VS Code

Configure VS Code to use these instructions for commit message generation:

1. Open VS Code Settings (`Ctrl+,` or `Cmd+,`)
2. Search for `github.copilot.chat.commitMessageGeneration.instructions`
3. Click **Edit in settings.json**
4. Add the following configuration:

```json
{
  "github.copilot.chat.commitMessageGeneration.instructions": [
    { "file": ".github/copilot-commit-message-instructions.md" }
  ]
}
```

> **Note:** Adjust the file path relative to your workspace root. If you copied this template to your project's `.github/` directory, use the path shown above.

## Customization

The template uses generic scope examples (`ui`, `vite-react`, `pnpm`). Adapt these to match your project structure:

- Update scope guidance to reflect your packages/modules
- Adjust examples to match your workflow
- Add project-specific commit types if needed

## How It Works

When configured via settings, VS Code automatically includes these instructions when:

- Using the **Source Control** view's sparkle icon to generate commit messages
- Asking Copilot Chat to generate commit messages
- Using the `Git: Commit Staged (AI Generated)` command

The instructions ensure consistent, well-structured commit messages following your team's conventions.

## Resources

- [VS Code Custom Instructions Documentation](https://code.visualstudio.com/docs/copilot/customization/custom-instructions#_specify-custom-instructions-in-settings)
- [Conventional Commits Specification](https://www.conventionalcommits.org/)
- [Awesome Copilot Templates](https://github.com/github/awesome-copilot)
