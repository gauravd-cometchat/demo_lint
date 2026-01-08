# Linting & Formatting Guide

## Available Commands

- `npm run lint` - Check for code quality issues (warnings only)
- `npm run lint:fix` - Automatically fix linting issues where possible
- `npm run format` - Format code with Prettier
- `npm run type-check` - Check TypeScript types

## IDE Setup

### VSCode

1. Install recommended extensions (prompt will appear automatically)
2. Format on save is enabled by default
3. ESLint will show warnings in real-time

### Other IDEs

- Install ESLint and Prettier plugins
- Enable format on save in your IDE settings

## Notes

- Linting errors are currently warnings only
- No git hooks are enforced yet
- Format your code before committing (optional but recommended)
- All existing code continues to work as-is

## Configuration Files

- `.eslintrc.json` - ESLint configuration
- `.prettierrc` - Prettier configuration
- `.eslintignore` - Files ignored by ESLint
- `.prettierignore` - Files ignored by Prettier
- `.vscode/settings.json` - VSCode IDE settings
- `.vscode/extensions.json` - Recommended VSCode extensions

## Troubleshooting

If you encounter issues:

1. Ensure you have the latest version of Node.js
2. Try running `npm install` to refresh dependencies
3. Check that your IDE has the ESLint and Prettier extensions installed
4. Restart your IDE after installing extensions

## Phase 1 Goals

This Phase 1 implementation focuses on:

- ✅ Basic linting with ESLint (warnings only)
- ✅ Code formatting with Prettier
- ✅ IDE integration for real-time feedback
- ✅ No workflow blocking or commit enforcement
- ✅ Gradual adoption without breaking existing code

Future phases will introduce stricter rules, git hooks, and CI/CD enforcement.
