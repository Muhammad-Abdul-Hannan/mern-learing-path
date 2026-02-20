# Node.js Learning – Day 2 Update

## 1️⃣ Working with Files (fs Module)

### fs vs fs/promises
- `fs` → callback-based file system operations.
- `fs/promises` → modern Promise-based API (recommended).

### File Operations Practiced
- `writeFile()` → create/overwrite file.
- `readFile()` → read file content.
- `appendFile()` → add content to existing file.
- `unlink()` → delete file.
- `access()` → check if file exists.

### Important Concepts
- Async file methods return Promises.
- `await` + `try/catch` handles rejected Promises.
- `writeFile()` creates file if it does not exist.
- `process.env` values are always strings.

---

## 2️⃣ Path Module

### What is path?
- Core Node module.
- Used to work with file and directory paths.
- Helps ensure cross-platform compatibility.

### Important Methods
- `path.join()` → safely combine paths.
- `path.resolve()` → return absolute path.
- `path.basename()` → get file name.
- `path.dirname()` → get directory.
- `path.extname()` → get extension.
- `path.parse()` → break path into parts.
- `path.format()` → rebuild path.

### Key Difference
- `join()` → combines paths.
- `resolve()` → gives absolute full path.

---

## 3️⃣ __dirname and __filename

- `__dirname` → folder of current file (CommonJS only).
- `__filename` → full path of current file.
- Not available in ES Modules (need workaround using `import.meta.url`).

---

## 4️⃣ Useful File & CLI Utilities

### glob
- Match files using patterns (e.g., `*.js`, `**/*.js`).

### globby
- Promise-based modern version of glob.

### fs-extra
- Extended fs module (copy, remove, ensureDir, etc.).

### chokidar
- Watch files/folders for changes (real-time file monitoring).

---

## 5️⃣ Command Line Applications (CLI)

### process.argv
- Contains command-line arguments.
- `process.argv[2]` onward → user inputs.

### readline Module
- Used to take interactive user input.
- Must call `rl.close()` after usage.

### Shebang (`#!/usr/bin/env node`)
- Makes script executable as a command.
- Needed when running file directly (not required when using `node file.js`).

---

## 6️⃣ Environment Variables

### What are Environment Variables?
- External configuration values.
- Used for secrets, ports, database URLs.

### process.env
- Object containing environment variables.
- All values are strings.

### .env File
- Stores environment variables in development.
- Requires `dotenv` package to load.

### Important Practice
- Never hardcode secrets.
- Add `.env` to `.gitignore`.
- Use fallback values:
  ```js
  const PORT = process.env.PORT || 3000;


7️⃣ Async Behavior Reminder
    await works only with Promises.
    Rejected Promise → treated like thrown error.
    try/catch works with await.
    Does NOT catch errors thrown inside async callbacks like setTimeout.


Today's Focus Summary
    Practical file handling
    Path manipulation
    CLI creation basics
    Understanding shebang
    Working with environment variables
    Using async/await properly with fs
