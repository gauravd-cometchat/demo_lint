# Phase 1 Linting & Formatting Setup Guide

This document provides step-by-step instructions to implement Phase 1 linting and formatting setup for TypeScript/React projects. Phase 1 focuses on **warnings only, no commit blocking, and gradual adoption** without breaking existing functionality.

## 🎯 Phase 1 Goals

- **Errors**: ❌ None enforced initially (0 errors in output)
- **Warnings**: ✅ Enabled for visibility only
- **No commit blocking**: ✅ Exit code 0 (success)
- **No large refactors**: ✅ All existing code continues to work
- **Production safety**: ✅ Nothing breaks existing functionality

## 📋 Prerequisites

- Node.js project with TypeScript
- React project (optional - can be adapted for other frameworks)
- Existing codebase that should continue working unchanged

## 🚀 Implementation Steps

### Step 1: Install Dependencies

```bash
npm install --save-dev eslint@^8.57.1 prettier@^3.7.4 @typescript-eslint/parser@^8.52.0 @typescript-eslint/eslint-plugin@^8.52.0 eslint-config-prettier@^10.1.8
```

### Step 2: Create ESLint Configuration

Create `.eslintrc.json` with **all rules set to "warn"**:

```json
{
  "root": true,
  "parser": "@typescript-eslint/parser",
  "parserOptions": {
    "ecmaVersion": 2022,
    "sourceType": "module"
  },
  "plugins": ["@typescript-eslint"],
  "extends": ["eslint:recommended", "plugin:@typescript-eslint/recommended", "prettier"],
  "rules": {
    // Override all error-level rules to warnings for Phase 1
    "@typescript-eslint/no-explicit-any": "warn",
    "@typescript-eslint/no-unused-vars": "warn",
    "@typescript-eslint/no-wrapper-object-types": "warn",
    "@typescript-eslint/no-unsafe-function-type": "warn",
    "@typescript-eslint/no-non-null-asserted-optional-chain": "warn",
    "@typescript-eslint/no-extra-non-null-assertion": "warn",
    "@typescript-eslint/no-empty-object-type": "warn",
    "@typescript-eslint/no-unused-expressions": "warn",
    "@typescript-eslint/no-require-imports": "warn",
    "@typescript-eslint/ban-ts-comment": "warn",
    "@typescript-eslint/no-this-alias": "warn",
    "@typescript-eslint/no-inferrable-types": "warn",
    "@typescript-eslint/no-namespace": "warn",
    "@typescript-eslint/no-var-requires": "warn",
    "@typescript-eslint/prefer-as-const": "warn",
    "prefer-const": "warn",
    "no-prototype-builtins": "warn",
    "no-empty": "warn",
    "no-useless-escape": "warn",
    "no-case-declarations": "warn",
    "no-var": "warn",
    "no-constant-condition": "warn",
    "no-unsafe-optional-chaining": "warn",
    "no-irregular-whitespace": "warn",
    "no-fallthrough": "warn",
    "no-global-assign": "warn",
    "no-redeclare": "warn",
    "no-self-assign": "warn",
    "no-unreachable": "warn",
    "no-unused-labels": "warn",
    "no-useless-catch": "warn",
    "no-mixed-spaces-and-tabs": "warn",
    "no-regex-spaces": "warn",
    "no-delete-var": "warn",
    "no-undef": "warn",
    "constructor-super": "warn",
    "for-direction": "warn",
    "getter-return": "warn",
    "no-async-promise-executor": "warn",
    "no-class-assign": "warn",
    "no-compare-neg-zero": "warn",
    "no-cond-assign": "warn",
    "no-const-assign": "warn",
    "no-control-regex": "warn",
    "no-debugger": "warn",
    "no-dupe-args": "warn",
    "no-dupe-class-members": "warn",
    "no-dupe-else-if": "warn",
    "no-dupe-keys": "warn",
    "no-duplicate-case": "warn",
    "no-empty-character-class": "warn",
    "no-empty-pattern": "warn",
    "no-ex-assign": "warn",
    "no-extra-boolean-cast": "warn",
    "no-extra-semi": "warn",
    "no-func-assign": "warn",
    "no-import-assign": "warn",
    "no-inner-declarations": "warn",
    "no-invalid-regexp": "warn",
    "no-loss-of-precision": "warn",
    "no-misleading-character-class": "warn",
    "no-new-symbol": "warn",
    "no-nonoctal-decimal-escape": "warn",
    "no-obj-calls": "warn",
    "no-octal": "warn",
    "no-promise-executor-return": "warn",
    "no-setter-return": "warn",
    "no-sparse-arrays": "warn",
    "no-this-before-super": "warn",
    "no-unexpected-multiline": "warn",
    "no-unreachable-loop": "warn",
    "no-unsafe-finally": "warn",
    "no-unsafe-negation": "warn",
    "no-useless-backreference": "warn",
    "use-isnan": "warn",
    "valid-typeof": "warn"
  },
  "env": {
    "browser": true,
    "es2022": true,
    "node": true
  },
  "globals": {
    "CometChat": "readonly",
    "NodeJS": "readonly",
    "JSX": "readonly",
    "EventListenerOrEventListenerObject": "readonly",
    "React": "readonly"
  }
}
```

**⚠️ Critical**: Adjust the `globals` section based on your project's global variables.

### Step 3: Create Prettier Configuration

Create `.prettierrc`:

```json
{
  "semi": true,
  "trailingComma": "es5",
  "singleQuote": true,
  "printWidth": 100,
  "tabWidth": 2,
  "useTabs": false
}
```

### Step 4: Create Ignore Files

Create `.eslintignore`:
```
node_modules/
dist/
build/
coverage/
*.min.js
```

Create `.prettierignore`:
```
node_modules/
dist/
build/
coverage/
package-lock.json
*.min.js
*.min.css
```

### Step 5: Add NPM Scripts

Add to `package.json`:

```json
{
  "scripts": {
    "lint": "eslint . --ext .ts,.tsx,.js,.jsx",
    "lint:fix": "eslint . --ext .ts,.tsx,.js,.jsx --fix",
    "format": "prettier --write \"**/*.{ts,tsx,js,jsx,json,css,scss,md}\"",
    "type-check": "tsc --noEmit"
  }
}
```

### Step 6: Create VSCode Integration

Create `.vscode/settings.json`:

```json
{
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": "explicit"
  },
  "eslint.validate": [
    "javascript",
    "javascriptreact",
    "typescript",
    "typescriptreact"
  ]
}
```

Create `.vscode/extensions.json`:

```json
{
  "recommendations": [
    "esbenp.prettier-vscode",
    "dbaeumer.vscode-eslint"
  ]
}
```

### Step 7: Create Documentation

Create `docs/LINTING.md`:

```markdown
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
```

## 🔧 Troubleshooting Common Issues

### Issue 1: ESLint Errors Instead of Warnings

**Problem**: ESLint shows errors instead of warnings
**Solution**: Ensure ALL rules in `.eslintrc.json` are set to `"warn"`, not `"error"`

### Issue 2: Unknown Global Variables

**Problem**: `'SomeGlobal' is not defined` errors
**Solution**: Add the global to the `globals` section in `.eslintrc.json`:

```json
"globals": {
  "YourGlobalVariable": "readonly"
}
```

### Issue 3: React Hooks Rules Not Found

**Problem**: `Definition for rule 'react-hooks/exhaustive-deps' was not found`
**Solution**: Remove any `/* eslint-disable react-hooks/... */` comments from files, or install `eslint-plugin-react-hooks`

### Issue 4: Build Still Failing

**Problem**: Build process fails due to linting
**Solution**: Verify `npm run lint` exits with code 0 (success). If not, check that all error rules are converted to warnings.

## ✅ Verification Steps

After setup, verify Phase 1 is working correctly:

1. **Run linting**: `npm run lint`
   - Should show **0 errors**
   - Should show warnings (any number is fine)
   - Should exit with code 0 (success)

2. **Run formatting**: `npm run format`
   - Should format files without errors
   - Should exit with code 0

3. **Run type checking**: `npm run type-check`
   - Should complete without errors
   - Should exit with code 0

4. **Run build**: `npm run build` (if applicable)
   - Should complete successfully
   - Should exit with code 0

## 🎯 Success Criteria

Phase 1 is successfully implemented when:

- ✅ `npm run lint` shows **0 errors** and exits with code 0
- ✅ All existing functionality continues to work unchanged
- ✅ IDE shows real-time warnings (not errors)
- ✅ Code formatting works with `npm run format`
- ✅ Build process remains unaffected
- ✅ No commit blocking or workflow interruption

## 🚀 Next Steps (Future Phases)
After Phase 1 is stable, consider:

- **Phase 2**: Convert critical warnings to errors
- **Phase 3**: Add git hooks for pre-commit linting
- **Phase 4**: Integrate with CI/CD pipeline
- **Phase 5**: Enforce stricter TypeScript rules

## 📝 Project-Specific Customizations

When using this guide, customize these sections for your project:

1. **Global Variables**: Update the `globals` section in `.eslintrc.json`
2. **File Extensions**: Adjust file patterns in scripts and ignore files
3. **Prettier Rules**: Modify `.prettierrc` to match your code style
4. **IDE Settings**: Adapt `.vscode/settings.json` for your workflow
5. **Documentation**: Update `docs/LINTING.md` with project-specific information

---

**Remember**: Phase 1 is about **gradual adoption** and **zero disruption**. The goal is to provide visibility into code quality without breaking existing workflows or functionality.