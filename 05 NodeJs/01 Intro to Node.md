# Node.js Learning – Day Update

## 1. Module Systems in Node.js
### CommonJS (CJS)
Uses `require()` and `module.exports`. Default module system in Node (unless `"type": "module"` is set).

### ES Modules (ESM)
Uses `import` and `export`. Enabled via `"type": "module"` in `package.json` or `.mjs` extension.

### module.exports vs exports
`module.exports` is the actual exported object. `exports` is just a reference to it (until reassigned).

### Default vs Named Exports
- `export default` → one primary export.
- `export { name }` → multiple named exports.
- Import syntax differs (`{}` for named, none for default).

### Re-exports
- `export * from` → re-export named exports.
- `export { default } from` → re-export default.
- Used for creating barrel (`index.js`) files.

---

## 2. Module Resolution
### Local Modules
Imported using relative paths (`./file.js`).

### Core Modules
Built-in Node modules like `fs`, `http`.

### Third-party Modules
Installed via npm and resolved from `node_modules`.

---

## 3. Error Handling in Node.js
### Synchronous Errors
Handled using `try/catch`.

### Callback Errors
Error-first pattern: `(err, data)`.

### Promise Errors
Handled using `.catch()` or `try/catch` with `await`.

### Async/Await Error Handling
`await` converts rejected Promises into thrown errors, catchable by `try/catch`.

### Uncaught Errors
- `process.on('uncaughtException')`
- `process.on('unhandledRejection')`

---

## 4. EventEmitter
### Basic Usage
- `on()` → listen to event
- `emit()` → trigger event
- `once()` → listen once
- `off()` → remove listener

### Important Behavior
- Synchronous execution.
- No memory of past events.
- Unhandled `'error'` event crashes Node.

---

## 5. Event Loop Basics
### Synchronous Execution
Runs first on the call stack.

### process.nextTick
Highest priority async queue in Node.

### Promise Microtasks
Run after `nextTick`, before timers.

### Timers Phase
Handles `setTimeout` and `setInterval`.

### Check Phase
Handles `setImmediate`.

### Key Order (Typical)
sync → nextTick → Promise → setTimeout → setImmediate

---

## 6. Async vs Callback Errors
- `try/catch` does NOT catch errors thrown inside async callbacks.
- Works with `await` because Promise rejections become thrown errors.

---

## 7. setTimeout(0) vs setImmediate
Both defer execution, but run in different event loop phases.
Order is not always guaranteed (except inside I/O callbacks).

---

### Today's Focus
- Deep understanding of module systems
- Proper async error handling
- EventEmitter fundamentals
- Event loop priority and execution order

---
