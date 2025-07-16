# gh-develop-with-prefix

A GitHub CLI extension that automatically prefixes branch names with your GitHub username when creating development branches from issues.

## Installation

### Install from GitHub

```bash
gh extension install razekmh/gh-develop-with-prefix
```

### Install from source

If you want to install from a local copy:

```bash
git clone https://github.com/razekmh/gh-develop-with-prefix.git
cd gh-develop-with-prefix
gh extension install .
```

## Usage

Use `gh develop-with-prefix` exactly like you would use `gh issue develop`, but with automatic username prefixing:

```bash
# Create a branch from issue #123
gh develop-with-prefix 123

# Create a branch with additional flags
gh develop-with-prefix --base main --checkout 456
```

### Shorter Aliases

For convenience, this extension also provides shorter aliases:

```bash
# Short alias
gh dev-prefix 123

# Even more intuitive (follows gh issue subcommand pattern)
gh issue dev-prefix 123
```

All three commands (`gh develop-with-prefix`, `gh dev-prefix`, `gh issue dev-prefix`) work identically.

## What it does

When you run `gh develop-with-prefix 123` on an issue titled "Add new feature":

- **Standard gh issue develop**: Creates branch `123-add-new-feature`
- **With this extension**: Creates branch `razekmh/123-add-new-feature`

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
# Basic usage (all equivalent)
gh develop-with-prefix 42
gh dev-prefix 42
gh issue dev-prefix 42

# With base branch
gh develop-with-prefix --base develop 42
gh dev-prefix --base develop 42
gh issue dev-prefix --base develop 42

# With checkout flag
gh develop-with-prefix --checkout 42
gh dev-prefix --checkout 42
gh issue dev-prefix --checkout 42

# Get help
gh develop-with-prefix --help
gh dev-prefix --help
gh issue dev-prefix --help
```

## Development

The extension is a bash script that wraps the `gh issue develop` command. It:

- Parses command line arguments
- Extracts the issue number
- Fetches your GitHub username and the issue title
- Constructs a prefixed branch name
- Passes all arguments through to `gh issue develop`

## Contributing

1. Fork the repository: https://github.com/razekmh/gh-develop-with-prefix
2. Create a feature branch: `git checkout -b feature/your-feature`
3. Make your changes
4. Test the extension locally: `gh extension install .`
5. Commit your changes: `git commit -am 'Add some feature'`
6. Push to the branch: `git push origin feature/your-feature`
7. Submit a pull request

## Repository

This extension is available on GitHub: https://github.com/razekmh/gh-develop-with-prefix

Browse the code, report issues, or contribute improvements!

## License

MIT License - see LICENSE file for details.
