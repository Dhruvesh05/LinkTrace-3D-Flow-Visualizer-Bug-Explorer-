# 🔗 LinkTrace — 3D Flow Visualizer & Bug Explorer

> Upload your codebase and watch it come alive: an interactive 3D graph of files and functions, paired with a lightweight static bug checker that flags common code smells before they bite you.

**TY Sem 5 — PBL Project**

[![Live Demo](https://img.shields.io/badge/demo-live-brightgreen)](https://link-trace-3-d-flow-visualizer-bug.vercel.app)
[![Next.js](https://img.shields.io/badge/frontend-Next.js-black?logo=next.js)](https://nextjs.org)
[![Express](https://img.shields.io/badge/backend-Express-yellow?logo=express)](https://expressjs.com)

**🌐 Live App:** [link-trace-3-d-flow-visualizer-bug.vercel.app](https://link-trace-3-d-flow-visualizer-bug.vercel.app)

---

## ✨ What is LinkTrace?

LinkTrace takes a set of source files (or a whole project folder) and:

1. **Parses** each file to extract the functions it defines.
2. **Builds a graph** connecting files to the functions inside them.
3. **Renders it in 3D** using a force-directed graph you can rotate, zoom, and explore.
4. **Scans for common issues** — TODOs, stray `console.log`s, suspicious imports, missing semicolons, and overly long lines — and reports them per file/line.

It's built as a learning project to make abstract codebase structure and quality feel tangible and explorable, rather than something you only read as a wall of text in a linter output.

---

## 🚀 Features

- 🌌 **3D force-directed graph** of files ↔ functions, powered by `react-force-graph-3d` and `three.js`
- 📁 **Drag-and-drop or folder upload**, with client-side filtering by file extension
- 🐞 **Static bug scanning** for `.js`, `.ts`, `.jsx`, `.tsx`, `.py`, `.java`, `.c`, and `.cpp` files
- 🎨 **Language-based color coding** in the graph for quick visual identification
- 🖥️ **Clean, animated landing page** built with Next.js + Tailwind CSS

---

## 🧱 Tech Stack

| Layer        | Technology |
|--------------|------------|
| Frontend     | [Next.js](https://nextjs.org) (App Router), React 19, Tailwind CSS |
| 3D Rendering | `three.js`, `react-force-graph-3d`, `react-force-graph-2d`, `three-spritetext` |
| Backend      | Node.js, Express |
| File Handling| `multer` (uploads), `unzipper` (archive extraction) |
| Tooling      | ESLint, Nodemon |

---

## 🗂️ Project Structure

```
LinkTrace-3D-Flow-Visualizer-Bug-Explorer/
├── backend/
│   ├── index.js              # Main server: upload, parse, bug-check, respond with graph + bug data
│   ├── routes/
│   │   └── bugPredict.js     # (WIP) route for an ML-based bug prediction service
│   └── uploads/              # Temp storage for uploaded files (cleared after processing)
│
└── frontend/
    └── src/
        ├── app/
        │   ├── page.js            # Landing page
        │   ├── upload/page.js     # Upload flow
        │   ├── visualizer/page.js # 3D visualizer page
        │   └── about/page.js      # About page
        └── components/
            ├── UploadSection.js       # File/folder upload + orchestration
            ├── CodeGraphVisualizer.js # 3D graph rendering
            ├── GraphVisualizer.js     # Graph data wiring
            ├── BugChecker.js          # Bug-check UI + results
            └── ErrorSection.js        # Error/bug log display
```

---

## ⚙️ Getting Started

### Prerequisites

- [Node.js](https://nodejs.org) v18+
- npm

### 1. Clone the repo

```bash
git clone https://github.com/Dhruvesh05/LinkTrace-3D-Flow-Visualizer-Bug-Explorer.git
cd LinkTrace-3D-Flow-Visualizer-Bug-Explorer
```

### 2. Set up the backend

```bash
cd backend
npm install
npm run dev   # starts with nodemon on http://localhost:5000
```

### 3. Set up the frontend

```bash
cd frontend
npm install
npm run dev   # starts Next.js on http://localhost:3000
```

By default, the frontend talks to `http://localhost:5000`. To point it elsewhere (e.g. a deployed backend), set:

```bash
# frontend/.env.local
NEXT_PUBLIC_BACKEND_URL=http://localhost:5000
```

### 4. Use it

Open [http://localhost:3000](http://localhost:3000), head to the upload section, drop in some source files (or a folder), and explore the generated 3D graph and bug report.

---

## 🔌 API Reference

### `POST /upload`

Accepts a multipart form with a `files` field (one or more files).

**Response:**

```json
{
  "graphData": {
    "nodes": [{ "id": "example.js", "functions": ["add", "subtract"] }],
    "links": [{ "source": "example.js", "target": "add" }]
  },
  "bugData": {
    "files": [
      {
        "name": "example.js",
        "errors": [
          { "line": 12, "column": 4, "message": "Unexpected console.log statement", "ruleId": "no-console" }
        ]
      }
    ]
  }
}
```

Supported extensions: `.js` `.ts` `.jsx` `.tsx` `.py` `.java` `.c` `.cpp`

---

## 🛣️ Roadmap

- [ ] Wire up `routes/bugPredict.js` to a real ML-based prediction service
- [ ] Support import/dependency edges between files (not just file → function)
- [ ] Persist and share visualizations via a shareable link
- [ ] Expand bug-detection rules beyond simple heuristics

---

## 🤝 Contributing

Contributions, issues, and feature requests are welcome. Feel free to fork the repo and open a pull request.

