# gh-develop-with-prefix

A GitHub CLI extension that automatically prefixes branch names with your GitHub username when creating development branches from issues.

## Installation

### Install from source

```bash
gh extension install /path/to/gh-develop-with-prefix
```

### Install from GitHub (after publishing)

```bash
gh extension install yourusername/gh-develop-with-prefix
```

## Usage

Use `gh develop-with-prefix` exactly like you would use `gh issue develop`, but with automatic username prefixing:

```bash
# Create a branch from issue #123
gh develop-with-prefix 123

# Create a branch with additional flags
gh develop-with-prefix --base main --checkout 456
```

## What it does

When you run `gh develop-with-prefix 123` on an issue titled "Add new feature":

- **Standard gh issue develop**: Creates branch `123-add-new-feature`
- **With this extension**: Creates branch `yourusername/123-add-new-feature`

## Requirements

- GitHub CLI (`gh`) installed and authenticated
- The repository must have issues enabled
- You must have permission to create branches in the repository

## How it works

1. Retrieves your GitHub username using `gh api user`
2. Fetches the issue title using `gh issue view`
3. Generates a branch name in the format: `username/issue-number-issue-title`
4. Calls `gh issue develop` with the prefixed branch name

## Examples

```bash
# Basic usage
gh develop-with-prefix 42

# With base branch
gh develop-with-prefix --base develop 42

# With checkout flag
gh develop-with-prefix --checkout 42

# Get help
gh develop-with-prefix --help
```

## Development

The extension is a bash script that wraps the `gh issue develop` command. It:

- Parses command line arguments
- Extracts the issue number
- Fetches your GitHub username and the issue title
- Constructs a prefixed branch name
- Passes all arguments through to `gh issue develop`

## Contributing

1. Fork the repository
2. Make your changes
3. Test the extension locally
4. Submit a pull request

## License

MIT License - see LICENSE file for details.
