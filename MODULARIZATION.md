# TuxMate Modularization Process

This document outlines the modularization and refactoring process for the TuxMate project, aimed at improving code maintainability, readability, and scalability.

## Overview

The modularization process is being conducted in phases to ensure minimal disruption to the existing codebase while systematically improving its structure and maintainability.

## Goals

1. **Consistent Code Formatting**: Implement Prettier for automatic code formatting across the entire codebase
2. **Modular Architecture**: Break down large files into smaller, reusable components
3. **Clean Code Principles**: Follow industry best practices for code organization and structure
4. **Maintainability**: Make the codebase easier to understand, test, and extend
5. **Documentation**: Provide clear documentation for all architectural decisions

## Phase 1: Prettier Integration ✅

### Completed Steps

1. **Prettier Installation**
   - Installed `prettier` as a dev dependency
   - Installed `eslint-config-prettier` to prevent ESLint conflicts with Prettier

2. **Configuration Files Created**
   - `.prettierrc`: Prettier configuration with project-specific formatting rules
   - `.prettierignore`: Files and directories to exclude from formatting

3. **Package Scripts Added**
   - `npm run format`: Format all files with Prettier
   - `npm run format:check`: Check if files are formatted correctly (useful for CI/CD)

4. **ESLint Integration**
   - Updated `eslint.config.mjs` to include `eslint-config-prettier`
   - This prevents ESLint from reporting errors for formatting rules that Prettier handles

5. **Initial Formatting**
   - Ran Prettier across the entire codebase
   - All files formatted according to the defined style guide

### Prettier Configuration Details

The project uses the following Prettier settings (`.prettierrc`):

```json
{
  "semi": true, // Use semicolons
  "trailingComma": "es5", // Trailing commas where valid in ES5
  "singleQuote": false, // Use double quotes
  "printWidth": 100, // Line length limit
  "tabWidth": 2, // 2 spaces for indentation
  "useTabs": false, // Use spaces, not tabs
  "arrowParens": "avoid", // Omit parens when possible in arrow functions
  "endOfLine": "lf" // Unix-style line endings
}
```

### Usage

#### Format all files

```bash
npm run format
```

#### Check if files are formatted (without modifying)

```bash
npm run format:check
```

#### Format specific files

```bash
npx prettier --write path/to/file.ts
```

### Integration with Development Workflow

- **Before Committing**: Run `npm run format` to ensure all code is formatted
- **CI/CD**: Use `npm run format:check` in CI pipelines to enforce formatting
- **Editor Integration**: Consider installing Prettier extensions for your editor:
  - VS Code: `esbenp.prettier-vscode`
  - WebStorm/IntelliJ: Built-in Prettier support
  - Vim: `prettier/vim-prettier`

## Phase 2: Code Modularization (Planned)

The next phase will focus on breaking down large files into smaller, focused modules.

### Target Files for Refactoring

1. **`src/app/page.tsx` (1,336 lines)**
   - Extract UI components into separate files
   - Separate business logic from presentation
   - Create reusable component library

2. **`src/lib/generateInstallScript.ts` (827 lines)**
   - Split script generation logic by distribution
   - Extract shared utilities
   - Create strategy pattern for different package managers

### Planned Structure

```
src/
├── components/
│   ├── ui/           # Shared UI components
│   ├── features/     # Feature-specific components
│   │   ├── distro-selector/
│   │   ├── app-catalog/
│   │   ├── script-generator/
│   │   └── how-it-works/
├── lib/
│   ├── script-generators/  # Distribution-specific script generators
│   │   ├── apt.ts
│   │   ├── pacman.ts
│   │   ├── dnf.ts
│   │   ├── flatpak.ts
│   │   └── snap.ts
│   ├── utils/       # Utility functions
│   └── types/       # TypeScript type definitions
└── hooks/           # Custom React hooks
```

### Refactoring Principles

- **Single Responsibility**: Each component/module should have one clear purpose
- **DRY (Don't Repeat Yourself)**: Extract common logic into reusable functions
- **Separation of Concerns**: Keep UI, business logic, and data separate
- **Type Safety**: Leverage TypeScript for better type inference and safety
- **Testability**: Write code that's easy to test in isolation

## Phase 3: Testing Infrastructure (Future)

- Set up Jest for unit testing
- Add React Testing Library for component testing
- Implement integration tests for critical flows
- Add pre-commit hooks with Husky for automated testing

## Phase 4: Documentation (Future)

- Add JSDoc comments to all public APIs
- Create component documentation with Storybook
- Document architectural decisions (ADRs)
- Create developer onboarding guide

## Code Review Requirements

**Important**: All pull requests related to modularization must:

1. ✅ Be reviewed and approved by @retrozenith (task requester)
2. ✅ Be reviewed and approved by the repository owner
3. ✅ Pass all linting checks (`npm run lint`)
4. ✅ Pass formatting checks (`npm run format:check`)
5. ✅ Include updated documentation where applicable

## Resources

- [Prettier Documentation](https://prettier.io/docs/en/index.html)
- [Clean Code Principles](https://github.com/ryanmcdermott/clean-code-javascript)
- [React Component Patterns](https://react.dev/learn/thinking-in-react)
- [Next.js Best Practices](https://nextjs.org/docs/architecture/nextjs-compiler)

## Questions or Suggestions?

Please open an issue or discussion in the repository to discuss any aspect of the modularization process.
