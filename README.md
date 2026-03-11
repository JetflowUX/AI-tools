# AI Tools Directory

A curated AI tools website built with Vue 3 and Vite.

The app organizes tools by category, supports instant search, provides light/dark theme switching, and is optimized for desktop and mobile browsing.

## Project Overview

- 20 categories of AI products
- 200 tools with descriptions, links, and tags
- Search by tool name, description, or tags
- Category jump navigation for fast browsing
- Light and dark mode toggle with saved preference
- Mobile-responsive layout

## Features

- Category-based directory for discovery
- Sticky header with category quick links
- Real-time filtering while typing
- External links for each tool card
- Clean card-based UI with tag metadata
- Theme preference persisted with localStorage

## Tech Stack

- Vue 3 (Composition API with script setup)
- Vite
- Plain CSS with design tokens

## Project Structure

```text
.
├── index.html
├── package.json
├── vite.config.js
└── src
		├── App.vue
		├── main.js
		├── style.css
		├── components
		│   ├── CategorySection.vue
		│   └── ToolCard.vue
		└── data
				└── tools.js
```

## Data Model

Tool data is defined in `src/data/tools.js` as category objects:

```js
{
	id: "category-id",
	name: "Category Name",
	icon: "🎯",
	description: "Category description",
	tools: [
		{
			name: "Tool Name",
			url: "https://example.com",
			description: "What this tool does",
			tags: ["tag1", "tag2"]
		}
	]
}
```

## Getting Started

### Prerequisites

- Node.js 18+ recommended
- npm

### Install

```bash
npm install
```

### Run Development Server

```bash
npm run dev
```

### Build for Production

```bash
npm run build
```

### Preview Production Build

```bash
npm run preview
```

## Customization

- Add or edit tools in `src/data/tools.js`
- Update global styles and theme tokens in `src/style.css`
- Adjust layout and filtering logic in `src/App.vue`
- Change category/tool presentation in `src/components/*`

## Notes

- This project is a curated directory and does not use a backend.
- All tool metadata is currently maintained in a local static data file.
