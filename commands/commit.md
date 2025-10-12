---
description: "API 文档生成：解析接口代码，比对并更新 docs/api.md"
argument-hint: [optional context...]
allowed-tools: Bash(git diff:*)
---

# Task: Generate a Conventional Commit Message

Based on the following code changes, please generate a concise and descriptive commit message that follows the Conventional Commits specification.

Provide only the commit message itself, without any introduction or explanation.

## Staged Changes:
!git diff --cached


## Unstaged Changes:
!git diff

## Output Format

### Single Type Changes

```
<emoji> <type>(<scope>): <subject>
  <body>
```

### Multiple Type Changes

```
<emoji> <type>(<scope>): <subject>
  <body of type 1>

<emoji> <type>(<scope>): <subject>
  <body of type 2>
...
```

## Type Reference

| Type     | Emoji | Description          | Example Scopes      |
| -------- | ----- | -------------------- | ------------------- |
| feat     | ✨     | New feature          | user, payment       |
| fix      | 🐛     | Bug fix              | auth, data          |
| docs     | 📝     | Documentation        | README, API         |
| style    | 💄     | Code style           | formatting          |
| refactor | ♻️     | Code refactoring     | utils, helpers      |
| perf     | ⚡️     | Performance          | query, cache        |
| test     | ✅     | Testing              | unit, e2e           |
| build    | 📦     | Build system         | webpack, npm        |
| ci       | 👷     | CI config            | Travis, Jenkins     |
| chore    | 🔧     | Other changes        | scripts, config     |
| i18n     | 🌐     | Internationalization | locale, translation |

## Writing Rules

### Subject Line

- Scope must be in English
- Imperative mood
- No capitalization
- No period at end
- Max 50 characters
- Must be in English

### Body

- Bullet points with "-"
- Max 72 chars per line
- Explain what and why
- Must be in English
- Use【】for different types

## Critical Requirements

1. Output ONLY the commit message
2. Write ONLY in English
3. NO additional text or explanations
4. NO questions or comments
5. NO formatting instructions or metadata

## Guidelines

- DO NOT add any ads such as "Generated with [Claude Code](https://claude.ai/code)"
- Only generate the message for staged files/changes
- Don't add any files using `git add`. The user will decide what to add. 
- Follow the rules below for the commit message.

## Examples

INPUT:

diff --git a/src/server.ts b/src/server.tsn index ad4db42..f3b18a9 100644n --- a/src/server.tsn +++ b/src/server.tsn @@ -10,7 +10,7 @@n import {n initWinstonLogger();
n n const app = express();
n -const port = 7799;
n +const PORT = 7799;
n n app.use(express.json());
n n @@ -34,6 +34,6 @@n app.use((\_, res, next) => {n // ROUTESn app.use(PROTECTED_ROUTER_URL, protectedRouter);
n n -app.listen(port, () => {n - console.log(`Server listening on port ${port}`);
n +app.listen(process.env.PORT || PORT, () => {n + console.log(`Server listening on port ${PORT}`);
n });

OUTPUT:

♻️ refactor(server): optimize server port configuration

- rename port variable to uppercase (PORT) to follow constant naming convention
- add environment variable port support for flexible deployment

Remember: All output MUST be in English language. You are to act as a pure commit message generator. Your response should contain NOTHING but the commit message itself.

## Optional User Context:
$ARGUMENTS