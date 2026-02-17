# 📦 NPM Learning Notes

These notes document my understanding of Node Package Manager (npm) while learning the MERN stack.

---

# 1️⃣ NPM Basics

## What is NPM?

NPM (Node Package Manager) is the default package manager for Node.js.

It is used to:
- Install packages
- Update packages
- Remove packages
- Manage dependencies
- Run project scripts

---

## package.json

`package.json` is the main configuration file of a Node.js project.

It stores:
- Project name and version
- Scripts (start, test, build, etc.)
- Dependencies
- devDependencies
- Project metadata (author, license, etc.)

Example:

```json
{
  "name": "my-app",
  "version": "1.0.0",
  "private": true,
  "scripts": {
    "start": "node index.js"
  },
  "dependencies": {
    "express": "^4.18.2"
  }
}
```

---

## package-lock.json

`package-lock.json` locks the exact versions of installed packages.

Why it matters:
- `package.json` allows version ranges (^, ~)
- `package-lock.json` locks exact versions
- Ensures everyone installs the same dependency versions

If someone runs:

```bash
npm install
```

They get the exact versions defined in `package-lock.json`.

---

## npm init

Initializes a new Node.js project.

```bash
npm init
```

Creates `package.json` after interactive questions.

Skip questions:

```bash
npm init -y
```

---

## npm install

Install a package:

```bash
npm install express
```

Install all dependencies:

```bash
npm install
```

Creates:
- node_modules/
- package-lock.json

---

## npm uninstall

```bash
npm uninstall express
```

Removes the package from dependencies.

---

## npm update

Update a specific package:

```bash
npm update express
```

Update all packages:

```bash
npm update
```

---

## Version Symbols

| Symbol | Allows Patch | Allows Minor | Allows Major |
|--------|--------------|--------------|--------------|
| ^      | ✅ Yes       | ✅ Yes       | ❌ No        |
| ~      | ✅ Yes       | ❌ No        | ❌ No        |

Install specific version:

```bash
npm install express@3.4.3
```

Install latest:

```bash
npm install express@latest
```

Install exact version (no ^):

```bash
npm install axios@1.3.2 --save-exact
```

---

# 2️⃣ Local vs Global Packages

## Local Packages

Installed per project:

```bash
npm install express
```

Used inside project files:

```js
require('express')
```

Each project can have different versions.

---

## Global Packages

Installed system-wide:

```bash
npm install -g nodemon
```

Accessible from terminal in any project.

🎯 Rule:
- Application libraries → Install locally
- CLI tools → Install globally

---

# 3️⃣ npx

npx = Node Package Executor.

Used to run a package without installing it globally.

Example:

```bash
npx create-react-app my-app
```

What happens:
1. Checks if package exists locally
2. If not, downloads temporarily
3. Executes it
4. May cache it

Before npx:

```bash
npm install -g create-react-app
create-react-app my-app
```

Now:

```bash
npx create-react-app my-app
```

---

# 4️⃣ node_modules Folder

Contains all installed packages and their dependency tree.

- Very large
- Can be regenerated using `npm install`
- Should NOT be committed to GitHub

Add to `.gitignore`:

```
node_modules/
```

---

# 5️⃣ Semantic Versioning (SemVer)

Format:

```
MAJOR.MINOR.PATCH
```

| Type  | Meaning |
|--------|---------|
| MAJOR | Breaking changes |
| MINOR | New features (backward compatible) |
| PATCH | Bug fixes |

Example:

```
4.18.2
```

- 4 → Major
- 18 → Minor
- 2 → Patch

---

# 6️⃣ Dependencies

## dependencies
Required to run the application.

Examples:
- express
- mongoose

---

## devDependencies
Used only during development.

Examples:
- eslint
- jest
- nodemon

Install:

```bash
npm install jest --save-dev
```

---

## peerDependencies

Means:

"I need this package to exist in the project, but I will not install it myself."

Common for plugins and libraries.

Example:

```json
"peerDependencies": {
  "react": "^18.0.0"
}
```

---

## optionalDependencies

Optional features.
If installation fails, project still works.

---

# 7️⃣ NPM Scripts

Defined inside `package.json`.

Example:

```json
"scripts": {
  "start": "node index.js",
  "dev": "nodemon index.js",
  "build": "webpack --mode production",
  "test": "jest"
}
```

Run:

```bash
npm start
npm run dev
npm test
```

Note:
- `start` and `test` don’t require `run`
- Others require `npm run`

---

## Pre and Post Scripts

Example:

```json
"scripts": {
  "prestart": "echo Preparing...",
  "start": "node index.js",
  "poststart": "echo Done"
}
```

Running:

```bash
npm start
```

Executes:

```
prestart → start → poststart
```

Used for automation tasks (cleanup, validation, etc.)

---

# 8️⃣ Package Management Commands

Install multiple packages:

```bash
npm install express mongoose cors
```

Remove package:

```bash
npm uninstall package-name
```

Update package:

```bash
npm update package-name
```

Check outdated packages:

```bash
npm outdated
```

List installed packages:

```bash
npm list --depth=0
```

Install only production dependencies:

```bash
npm install --omit=dev
```

---

# 9️⃣ NPM Config

Check config:

```bash
npm config list
```

Set registry:

```bash
npm config set registry <url>
```

`.npmrc` file stores npm configuration.

Global config → affects system  
Local config → affects project only

---

# 🔟 Publishing Packages

Login:

```bash
npm login
```

Publish:

```bash
npm publish
```

Scoped package format:

```
@username/package-name
```

Increase version:

```bash
npm version patch
npm version minor
npm version major
```

Unpublish (limited time window):

```bash
npm unpublish package-name
```

---

# 1️⃣1️⃣ Security & Maintenance

Audit packages:

```bash
npm audit
```

Fix issues:

```bash
npm audit fix
```

⚠ `--force` may introduce breaking changes.

Lock file ensures consistent installs across environments.

Dependency tree = package → sub-packages structure.

---

# 1️⃣2️⃣ Workspaces

Workspaces allow managing multiple packages inside one repo (monorepo).

Example structure:

```
project-root/
  package.json
  frontend/
    package.json
  backend/
    package.json
```

Root `package.json`:

```json
{
  "private": true,
  "workspaces": ["frontend", "backend"]
}
```

Now running:

```bash
npm install
```

Installs dependencies for both.

---

# 1️⃣3️⃣ npm link

Used for local package development without publishing.

In library folder:

```bash
npm link
```

In app folder:

```bash
npm link your-library-name
```

Creates a symlink so changes reflect immediately.

---

# 1️⃣4️⃣ Creating CLI Tools

Key concepts:
- `bin` field in package.json
- Shebang line:

```js
#!/usr/bin/env node
```

- process.argv (for arguments)
- commander / yargs (argument parsing)
- chalk (output styling)
- inquirer (user prompts)

Run without global install:

```bash
npx my-cli
```

---

# 1️⃣5️⃣ Environment Variables

Never hardcode secrets.

Use `.env` file:

```
PORT=5000
MONGO_URI=your_mongodb_url
JWT_SECRET=secretkey
```

Install dotenv:

```bash
npm install dotenv
```

Use in code:

```js
require('dotenv').config();
process.env.PORT
```

Add `.env` to `.gitignore`.

---

# 1️⃣6️⃣ Best Practices

- Keep dependencies minimal
- Remove unused packages
- Commit:
  - package.json
  - package-lock.json
- Do NOT commit:
  - node_modules/
- Use meaningful script names (dev, build, lint, test)
- Add `"private": true` if not publishing

Example `.gitignore`:

```
node_modules/
.env
dist/
build/
```

---

## Final Note

These notes are part of my MERN learning journey.
The goal is to deeply understand package management and maintain clean, scalable JavaScript projects.
