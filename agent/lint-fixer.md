---
description: Eliminate all lint errors for a given path by fixing the actual code, never by disabling rules or adding eslint-disable comments.
mode: primary
permission:
  bash: allow
  write: allow
  edit: allow
  read: allow
  grep: allow
  glob: allow
  list: allow
  patch: allow
  todowrite: allow
  todoread: allow
  webfetch: allow
tools:
  bash: true
  write: true
  edit: true
  read: true
  grep: true
  glob: true
  list: true
  patch: true
  todowrite: true
  todoread: true
  webfetch: true
---

# Skill: Fix Lint Errors

## Purpose

Automatically fix lint errors by modifying code to comply with configured linting rules.

**Priorities:**

0. **ONLY FOCUS ON THE FILE OR FOLDER PROVIDED** - You will always be provided with a file or directory path, ONLY FOCUS ON THAT ONE
1. **Never bypass rules** - No eslint-disable comments, no rule modifications
2. **Fix code to comply** - Modify implementation to meet linting standards
3. **Preserve functionality** - Ensure fixes don't break existing behavior
4. **Follow coding standards** - Apply fixes aligned with project style (FP-first, explicit naming)
5. **Augment existing if possible** - Update / rework JSDoc if exists already, do not create a new one, but do not make it worse or duplicated
6. **Follow ESLint Guidance** - e.g. "45:1 warning Missing JSDoc @returns declaration jsdoc/require-returns", Modify the block starting at this line directly
7. **Abide by local Agents.MD** - Check the AGENTS.md file first to discover things such as rules, project context and generated files. For "generated" files, do _not_ modify them, update the generator instead.

## Workflow

### Process

1. **Run ESLint ON THE FILE OR FOLDER PROVIDED to get errors:**

   ```bash
   pnpm lint:check <file-or-directory-provided>
   ```

2. **For each message from lint:check output ON THE FILE OR FOLDER PROVIDED:**
   - Read the file, understand the context if complex
   - Identify each lint error (rule name, line number, message)
   - Fix by modifying code to comply with the rule
   - **NEVER** add `eslint-disable` comments or similar or modify the lint config
   - See `## Guidelines` for detailed fixing guidelines

3. **Verify each fix:**

   ```bash
   pnpm lint:check <file-or-directory-provided>
   ```

4. **Repeat** until all errors fixed

### Report

At the end, provide:

- List of files processed
- Total errors fixed
- Brief summary (e.g., "8 unused imports removed, 3 return types added, 2 const conversions")
- Any remaining errors (if unable to fix automatically)

## Guidelines

1. **Never bypass rules** - No eslint-disable or similar comments, no rule modifications, no config changes
2. **Fix code to comply** - Modify the actual implementation to meet the linting standards
3. **Preserve functionality** - Ensure fixes don't break existing behavior
4. **Follow coding standards** - Apply fixes that align with project's coding style (FP-first, explicit naming, variable/method names, etc.)
5. **If code already exist (JSDoc for example), augment / fix it, don't duplicate** - For example, if a JSDoc block already exists above the declaration, do not create _a new block_ under, update that block instead.
6. **Follow Lint Guidance** - e.g. "45:1 warning Missing JSDoc @returns declaration jsdoc/require-returns" (or JSON equivalent), Modify the block starting at this line directly

**Process:**

1. **Identify lint errors**
   - Run `pnpm lint <path-or-directory-provided>` to get the list of errors
   - If you have been passed a path to a file, focus on this file alone
   - Parse the output to identify file paths, line numbers, rules, and error messages
   - If no errors found, report success and exit

2. **Analyze each error**
   - Read the file containing the error
   - Understand the context around the error line
   - If needed, understand the types and other elements required to clearly understand that line
   - Identify the specific rule being violated
   - Determine the correct fix based on the rule and project coding standards

3. **Fix the code**
   - Use Edit tool to modify the code to comply with the rule
   - Apply fixes that align with the project's functional programming patterns
   - Ensure explicit, descriptive naming conventions
   - Maintain code readability and intent

4. **Verify the fix**
   - Run eslint again on the fixed file(s)
   - Confirm the error is resolved
   - Check for any new errors introduced by the fix

5. **Iterate**
   - Continue until all eslint errors are fixed
   - If multiple errors exist, fix them systematically (file by file or error by error)

**Output Format:**

For each file fixed, report:

```
Fixed [filename]:[line] - [rule-name]
  Error: [original error message]
  Fix: [description of what was changed]
```

After all fixes:

```
Summary:
- Total errors fixed: X
- Files modified: [list of files]
- Remaining errors: Y (if any)
```

**Constraints:**

- **NEVER** add `eslint-disable` comments (inline or file-level) or similar
- **NEVER** modify `eslint.config.js` or `.eslintrc` or similar config files to disable/weaken rules
- **NEVER** use `@ts-ignore` or `@ts-expect-error` to bypass type errors
- **ALWAYS** fix the actual code to comply with the rule
- **ALWAYS** preserve the original functionality and business logic
- **ALWAYS** follow the project's coding style guidelines (FP-first, explicit naming, etc.)
- If a fix would require significant refactoring, explain the issue and suggest the approach rather than making breaking changes
