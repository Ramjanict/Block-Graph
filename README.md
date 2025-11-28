# Block Graph

Live demo: https://block-graph-seven.vercel.app

GitHub: https://github.com/Ramjanict/Block-Graph

---

## What is this

**Block Graph** is a small interactive React app that lets you create draggable blocks and visually connect them to their parent. When the page loads a block appears at a random position. Each block has a `+` button — clicking it creates a child block (also placed randomly) and draws a dashed connector line from the parent to the child. Connectors update automatically when either block is dragged.

This repo was built with React + Tailwind and uses a lightweight state-management approach to store blocks and relationships. No UI libraries other than Tailwind are used.

---

## Key features

- A block appears at a random position when the page opens.
- Each block has a `+` button that spawns a child block in a random position.
- Blocks are draggable with the mouse.
- Each child block draws a dashed line connecting to its parent block.
- Lines follow blocks when parents or children are moved.
- Built using React + Tailwind; any state-management library can be swapped in.

---

## Tech stack

- React (Vite / Create React App — depending on the starter code present in the repo)
- Tailwind CSS
- Plain JavaScript / TypeScript for drag & connector logic
- Optional: small state library (Zustand / Redux / Context) — the project keeps state separate so you can switch easily.

---

## Live preview

Open the deployed demo: https://block-graph-seven.vercel.app

---

## Quick start — run locally

> These commands assume you have Node.js >= 16 and npm or yarn installed.

```bash
# 1. Clone the repo
git clone https://github.com/Ramjanict/Block-Graph.git
cd Block-Graph

# 2. Install dependencies
npm install
# or
# yarn

# 3. Start dev server
npm run dev
# or
# npm run start
```

Open `http://localhost:5173` (Vite) or `http://localhost:3000` depending on the project starter.

---

## Project structure (suggested)

```
/src
  /components
    Block.jsx         # Single draggable block component
    Connector.jsx     # SVG/Canvas component that draws dashed lines between nodes
    Board.jsx         # Main area that renders all blocks and connectors
  /store
    useBlocks.js      # Centralized state for blocks & relationships (Zustand / Context)
  utils
    math.js           # helper functions (distance, angle, randomPosition)
  App.jsx
  main.jsx

public
  index.html

README.md
package.json
```

> The exact filenames may differ from the starter code. The structure above describes the responsibilities of each area.

---

## Implementation notes / tips

- **Block identity**: each block uses a unique id and stores `{ id, x, y, parentId }`.
- **Random placement**: when spawning place the block within the board bounds (subtract block size) to avoid overflow.
- **Dragging**: keep dragging logic in the `Block` component and update the central store with the new coordinates so connectors can re-render.
- **Connector drawing**: use an SVG layer over the board (or under it) to draw `<line>` elements from parent center to child center. Update the `x1,y1,x2,y2` attributes from the store positions.
- **Performance**: for many nodes consider debouncing updates or rendering connectors in a single SVG with a lightweight renderer.

---

## Customization ideas / roadmap

- Add a context-menu on blocks (rename, delete, reparent).
- Allow dragging a block to another block to change parent.
- Snap-to-grid option and alignment guides.
- Persist layout (localStorage or backend) and load saved graphs.
- Add zoom & pan for large graphs.

---

## Troubleshooting

- If blocks sometimes spawn off-screen, adjust the random position bounds to account for the block width/height and board padding.
- If connectors lag while dragging, try updating positions at animation frame frequency using `requestAnimationFrame`.

---

## Contributing

Contributions are welcome. Open an issue or a PR with a clear description of the change. If you want to extend state-management, add tests, or improve performance, please describe the approach in an issue first.

---

## License

This project is released under the MIT License. See the `LICENSE` file for details.

---

## Author / Contact

Md Ramjan — feel free to open issues or PRs on GitHub: https://github.com/Ramjanict/Block-Graph
