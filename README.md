# 🧩 NodeFlow — Interactive Block Graph Builder

> A zero-dependency visual node editor built with React, TypeScript, and Tailwind CSS. Create, connect, and freely drag hierarchical block graphs on a canvas.

[![Live Demo](https://img.shields.io/badge/Live%20Demo-Vercel-000?style=for-the-badge&logo=vercel)](https://block-graph-seven.vercel.app)
[![GitHub](https://img.shields.io/badge/GitHub-Ramjanict-181717?style=for-the-badge&logo=github)](https://github.com/Ramjanict/Block-Graph)
[![React](https://img.shields.io/badge/React-18-61DAFB?style=for-the-badge&logo=react)](https://reactjs.org)
[![TypeScript](https://img.shields.io/badge/TypeScript-5-3178C6?style=for-the-badge&logo=typescript)](https://www.typescriptlang.org)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind-3-06B6D4?style=for-the-badge&logo=tailwindcss)](https://tailwindcss.com)
[![Vite](https://img.shields.io/badge/Vite-4-646CFF?style=for-the-badge&logo=vite)](https://vitejs.dev)

---

## ✨ Overview

**NodeFlow** is a lightweight, interactive canvas application that lets you build and visualize tree-structured node graphs directly in the browser. It starts with a single root block and lets you expand it into a full hierarchy — every child is connected to its parent via a live-updating dashed SVG connector line.

Perfect as a foundation for **mind maps**, **workflow builders**, **dependency visualizers**, or **UI tree editors**.

---

## 🚀 Live Demo

👉 **[https://block-graph-seven.vercel.app](https://block-graph-seven.vercel.app)**

---

## 🎯 Features

| Feature | Details |
|---|---|
| **Spawn Blocks** | Click `+` on any block to add a child node at an auto-offset position |
| **Drag & Drop** | Freely drag any block anywhere on the canvas via native mouse events |
| **Live Connectors** | Dashed SVG polyline connectors update in real-time as blocks are moved |
| **Hierarchical Layout** | Child blocks are offset horizontally and vertically from their parent |
| **Zero Dependencies** | No external graph or drag-and-drop library — pure React + SVG |
| **Full-Screen Canvas** | Full-viewport pink canvas with overflow clipping |
| **TypeScript** | Fully typed components and state |

---

## 🛠️ Tech Stack

| Technology | Version | Purpose |
|---|---|---|
| [React](https://reactjs.org) | 18.x | UI rendering & component state |
| [TypeScript](https://www.typescriptlang.org) | 5.x | Type safety |
| [Vite](https://vitejs.dev) | 4.x | Dev server & build tool |
| [Tailwind CSS](https://tailwindcss.com) | 3.x | Utility-first styling |
| [ESLint](https://eslint.org) | 8.x | Code quality |

---

## 📁 Project Structure

```
Block-Graph/
├── public/
│   └── vite.svg
├── src/
│   ├── components/
│   │   ├── Block.tsx           # Draggable block node with + spawn button
│   │   ├── BlocksCanvas.tsx    # Main canvas — manages block state & layout
│   │   └── ConnectionLines.tsx # SVG polyline connector between parent & child
│   ├── App.tsx                 # Root component
│   ├── main.tsx                # React entry point
│   ├── index.css               # Global styles
│   └── vite-env.d.ts
├── index.html
├── package.json
├── tailwind.config.js
├── tsconfig.json
├── vite.config.ts
└── vercel.json
```

---

## ⚡ Getting Started

> **Prerequisites:** Node.js >= 16, npm >= 8

```bash
# 1. Clone the repository
git clone https://github.com/Ramjanict/Block-Graph.git
cd Block-Graph

# 2. Install dependencies
npm install

# 3. Start the development server
npm run dev
```

Open **[http://localhost:5173](http://localhost:5173)** in your browser.

### Available Scripts

| Command | Description |
|---|---|
| `npm run dev` | Start Vite dev server with HMR |
| `npm run build` | Type-check and build for production |
| `npm run preview` | Preview the production build locally |
| `npm run lint` | Lint all `.ts` / `.tsx` files |

---

## 🏗️ Architecture

### Component Responsibilities

```
BlocksCanvas (State Owner)
├── Block[]            — renders each draggable node
│     └── onAdd()      — spawns a child with offset position
│     └── onDrag()     — updates x/y in canvas state
└── ConnectionLine[]   — SVG polyline per parent-child relationship
      └── startX/Y     — bottom-center of parent block
      └── endX/Y       — top-center of child block
      └── midY bezier  — creates orthogonal step connector
```

### Block Data Shape

```ts
interface BlockType {
  id: number;      // unique auto-incremented identifier
  x: number;       // absolute left position (px)
  y: number;       // absolute top position (px)
  parentId?: number; // undefined for root block
}
```

### Connector Geometry

The `ConnectionLine` component draws an **orthogonal (step) polyline** using four points:

```
(startX, startY)  →  (startX, midY)  →  (endX, midY)  →  (endX, endY)
     ↓                                                          ↑
  parent bottom-center                                   child top-center
```

---

## 🔭 Roadmap / Ideas

- [ ] Delete blocks (with cascade removal of children)
- [ ] Rename blocks inline
- [ ] Drag-to-reparent between blocks
- [ ] Snap-to-grid & alignment guides
- [ ] Zoom & pan (canvas transform)
- [ ] Persist layout to `localStorage` or a backend
- [ ] Export graph as JSON or PNG
- [ ] Curved bezier connectors (toggle with orthogonal)
- [ ] Undo / redo history

---

## 🐞 Known Issues & Tips

- **Block spawns off-screen?** The random offset on child placement uses parent position + fixed offsets. Adjust `offsetX` / `offsetY` in `BlocksCanvas.tsx` for tighter layouts.
- **Connector lag during fast drag?** Wrap the state update in `requestAnimationFrame` for smoother re-renders on high-node-count graphs.

---

## 🤝 Contributing

Contributions, issues, and feature requests are welcome!

1. Fork the repo
2. Create a feature branch: `git checkout -b feature/my-feature`
3. Commit your changes: `git commit -m 'feat: add my feature'`
4. Push to the branch: `git push origin feature/my-feature`
5. Open a Pull Request

Please open an issue first for large changes to discuss the approach.

---

## 📄 License

Released under the **MIT License** — see [`LICENSE`](LICENSE) for details.

---

## 👤 Author

**Md Ramjan**
- GitHub: [@Ramjanict](https://github.com/Ramjanict)
- Project: [Block-Graph](https://github.com/Ramjanict/Block-Graph)

---

> **Tags:** `react` `typescript` `vite` `tailwindcss` `node-graph` `block-editor` `canvas` `drag-and-drop` `svg` `visual-programming` `mind-map` `workflow-builder` `tree-view` `interactive-ui` `frontend`
