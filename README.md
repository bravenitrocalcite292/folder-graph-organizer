# Folder Graph Organizer

An [Obsidian](https://obsidian.md) plugin that automatically creates **folder index notes** and links every note, canvas, and subfolder back to them — turning Obsidian's Graph View into a clean, hub-and-spoke map of your entire vault.

![Obsidian](https://img.shields.io/badge/Obsidian-Plugin-7C3AED?logo=obsidian&logoColor=white)
![Version](https://img.shields.io/github/v/release/jacobbarcys-dot/folder-graph-organizer)
![License](https://img.shields.io/github/license/jacobbarcys-dot/folder-graph-organizer)

---

## What it does

For every folder in your vault, the plugin:

1. **Creates an index note** named after the folder (e.g. `Projects/Projects.md`)
2. **Links every note** in that folder back to the index with an `up::` property
3. **Links every canvas** in that folder into the index note
4. **Chains subfolders** — each subfolder's index gets an `up::` link to the parent index, building a full hierarchy
5. **Assigns a unique color tag** (`folder-color-1` through `folder-color-8`) to each index note so you can give every folder cluster its own color in Graph View

The result in Graph View is a **cluster of connected nodes for every folder**, with the index note as the large central hub.

---

## Recommended companion plugin

> 🗂️ **Install [Folder Notes](https://github.com/LostPaul/obsidian-folder-notes) by LostPaul for the best experience.**

Because index notes are named after their folder and placed inside it, the Folder Notes plugin recognises them automatically — no extra configuration needed. Once installed:

- Clicking a **folder** in the file explorer opens its index note directly
- The folder acts like a page, just like Notion or Craft
- Your vault feels fully navigable without ever touching Graph View

The two plugins were designed to work together out of the box.

---

## Features

| Feature | Details |
|---|---|
| 📄 Folder-named indexes | Each index is named after its folder, not a generic `_Index` |
| 🔗 Auto-linking | Notes get `up:: [[FolderName]]` prepended on creation |
| 🗺️ Canvas support | `.canvas` files are listed in the folder index |
| 🌲 Subfolder chaining | Subfolder indexes link up to their parent |
| 🎨 Per-folder colors | 8 color tags assigned by folder name for Graph View groups |
| ⚡ Auto-link on create | New notes and canvases are linked instantly |
| 📊 Dashboard | Visual overview of all folders, their note counts, and index status |

---

## Installation

### Via BRAT (recommended for now)

1. Install [BRAT](https://github.com/TfTHacker/obsidian42-brat) from Community Plugins
2. Open BRAT settings → **Add Beta Plugin**
3. Paste: `https://github.com/jacobbarcys-dot/folder-graph-organizer`
4. Enable the plugin in Settings → Community Plugins

### Manual installation

1. Download `main.js`, `manifest.json`, and `styles.css` from the [latest release](https://github.com/jacobbarcys-dot/folder-graph-organizer/releases/latest)
2. Create a folder: `<your vault>/.obsidian/plugins/folder-graph-organizer/`
3. Copy the three files into that folder
4. Reload Obsidian and enable the plugin

---

## Usage

### First-time setup

1. Open the **Folder Graph Organizer** dashboard (ribbon icon or command palette)
2. Click **"Create All Index Notes"** to create an index in every folder
3. Click **"Scan & Link Everything"** to link all existing notes and canvases
4. Open Graph View — your vault is now organised into folder clusters

### Ongoing use

With **Auto-link on create** enabled (default), any new note or canvas you create is automatically linked to its folder index. You don't need to run any commands manually.

### Commands

| Command | What it does |
|---|---|
| Create index note for current folder | Creates an index for the folder of the active note |
| Create index notes for all folders | Creates indexes for every folder that doesn't have one |
| Scan vault and link all notes | Links all existing notes and canvases to their folder indexes |
| Open Folder Graph dashboard | Opens the visual overview panel |

---

## Graph View — color setup

Each index note is tagged with `folder-color-1` through `folder-color-8` based on the folder name. To make each folder cluster a different colour:

1. Open **Graph View** → click the sliders icon → **Groups**
2. Add a group, set the query to `tag:folder-color-1`, pick a colour
3. Repeat for `folder-color-2` through `folder-color-8`
4. Add one more group: `tag:folder-index` with a large node size to make hubs stand out

The colour assigned to each folder is stable — it won't change unless you rename the folder.

---

## Settings

| Setting | Default | Description |
|---|---|---|
| Backlink property | `up` | The inline property added to notes linking back to their index |
| Index note tag | `folder-index` | Tag applied to all index notes |
| Link subfolders to parent | On | Chains subfolder indexes to the parent index |
| Link canvas files | On | Adds canvas files to the folder index |
| Auto-link new files | On | Automatically links new notes and canvases on creation |

---

## How it works

When you run **Scan & Link Everything**, the plugin:

1. Walks every folder in your vault (deepest first)
2. Creates an index note named `FolderName.md` inside the folder if one doesn't exist
3. Prepends `up:: [[FolderName]]` to every note in the folder
4. Adds `[[CanvasName.canvas]]` entries under `## Canvases` in the index
5. Adds `[[SubfolderName]]` entries under `## Subfolders` in the index
6. Links the subfolder's own index up to the parent with `up:: [[ParentFolderName]]`

All index notes include `tags: [folder-index, folder-color-N]` in their frontmatter so they can be targeted in Graph View groups.

---

## Building from source

```bash
git clone https://github.com/jacobbarcys-dot/folder-graph-organizer.git
cd folder-graph-organizer
npm install
node esbuild.config.mjs production
```

The compiled output is `main.js`. Copy `main.js`, `manifest.json`, and `styles.css` to your vault's plugin folder.

---

## License

MIT
