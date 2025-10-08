# Tic Tac Toe - Vue 3 Application

A modern, responsive Tic Tac Toe game built with Vue 3, TypeScript, and Vite, featuring the Ocean Professional theme.

## Features

- 🎮 Classic Tic Tac Toe gameplay
- 🎨 Modern UI with Ocean Professional theme (blue and amber accents)
- ✨ Smooth animations and transitions
- 📱 Fully responsive design (desktop, tablet, mobile)
- 🏆 Win detection across rows, columns, and diagonals
- 🤝 Draw detection
- 🔄 Reset/New Game functionality
- ♿ Accessible and user-friendly interface

## Tech Stack

- **Vue 3** - Progressive JavaScript framework
- **TypeScript** - Type-safe development
- **Vite** - Next-generation frontend tooling
- **Pinia** - State management (included but not required for this app)
- **Vue Router** - Routing (included but not required for this app)

## Getting Started

### Prerequisites

- Node.js (v18 or higher recommended)
- npm (comes with Node.js)

### Installation

```sh
npm install
```

### Development

Start the development server with hot-reload:

```sh
npm run dev
```

The application will be available at `http://localhost:3000`

### Build for Production

Type-check, compile, and minify for production:

```sh
npm run build
```

### Preview Production Build

Preview the production build locally:

```sh
npm run preview
```

## Project Structure

```
src/
├── components/
│   └── TicTacToe.vue       # Main game component
├── assets/
│   └── main.css            # Global styles with Ocean Professional theme
├── App.vue                 # Root component
└── main.ts                 # Application entry point
```

## Game Rules

1. The game is played on a 3x3 grid
2. Players take turns placing their mark (X or O)
3. The first player to get 3 marks in a row (horizontally, vertically, or diagonally) wins
4. If all 9 cells are filled and no player has won, the game is a draw
5. Click "Reset Game" or "New Game" to start over

## Theme - Ocean Professional

- **Primary Color**: Blue (#2563EB)
- **Secondary Color**: Amber (#F59E0B)
- **Background**: Light gray (#f9fafb)
- **Surface**: White (#ffffff)
- **Text**: Dark gray (#111827)
- **Style**: Modern with subtle gradients, rounded corners, and soft shadows

## Additional Commands

### Run Unit Tests

```sh
npm run test:unit
```

### Lint and Format

```sh
npm run lint
npm run format
```

### Type-Check

```sh
npm run type-check
```

## Browser Support

- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)

## License

Private project

## Acknowledgments

Built with Vue 3 and Vite template for Kavia platform.
