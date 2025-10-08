<script setup lang="ts">
import { ref, computed } from 'vue'

// PUBLIC_INTERFACE
/**
 * TicTacToe Component
 * Implements a complete Tic Tac Toe game with win/draw detection and turn management
 */

// Game state
const board = ref<(string | null)[]>(Array(9).fill(null))
const currentPlayer = ref<'X' | 'O'>('X')
const winner = ref<string | null>(null)
const isDraw = ref(false)

// Winning combinations
const winningCombinations = [
  [0, 1, 2], // Top row
  [3, 4, 5], // Middle row
  [6, 7, 8], // Bottom row
  [0, 3, 6], // Left column
  [1, 4, 7], // Middle column
  [2, 5, 8], // Right column
  [0, 4, 8], // Diagonal top-left to bottom-right
  [2, 4, 6]  // Diagonal top-right to bottom-left
]

// Computed property for game status message
const statusMessage = computed(() => {
  if (winner.value) {
    return `Player ${winner.value} Wins! 🎉`
  }
  if (isDraw.value) {
    return "It's a Draw! 🤝"
  }
  return `Current Player: ${currentPlayer.value}`
})

// Check for winner
const checkWinner = (): string | null => {
  for (const combination of winningCombinations) {
    const [a, b, c] = combination
    if (
      board.value[a] &&
      board.value[a] === board.value[b] &&
      board.value[a] === board.value[c]
    ) {
      return board.value[a]
    }
  }
  return null
}

// Check for draw
const checkDraw = (): boolean => {
  return board.value.every(cell => cell !== null) && !winner.value
}

// Handle cell click
const handleCellClick = (index: number) => {
  // Ignore click if cell is already filled or game is over
  if (board.value[index] || winner.value || isDraw.value) {
    return
  }

  // Place the current player's mark
  board.value[index] = currentPlayer.value

  // Check for winner
  const gameWinner = checkWinner()
  if (gameWinner) {
    winner.value = gameWinner
    return
  }

  // Check for draw
  if (checkDraw()) {
    isDraw.value = true
    return
  }

  // Switch player
  currentPlayer.value = currentPlayer.value === 'X' ? 'O' : 'X'
}

// Reset game
const resetGame = () => {
  board.value = Array(9).fill(null)
  currentPlayer.value = 'X'
  winner.value = null
  isDraw.value = false
}
</script>

<template>
  <div class="game-container">
    <h1 class="game-title">Tic Tac Toe</h1>
    
    <!-- Status Display -->
    <div 
      class="status-display" 
      :class="{
        'status-winner': winner,
        'status-draw': isDraw,
        'status-playing': !winner && !isDraw
      }"
    >
      {{ statusMessage }}
    </div>

    <!-- Game Board -->
    <div class="game-board">
      <button
        v-for="(cell, index) in board"
        :key="index"
        class="cell"
        :class="{
          'cell-x': cell === 'X',
          'cell-o': cell === 'O',
          'cell-empty': !cell,
          'cell-disabled': winner || isDraw
        }"
        @click="handleCellClick(index)"
        :disabled="!!cell || !!winner || isDraw"
      >
        {{ cell }}
      </button>
    </div>

    <!-- Reset Button -->
    <button class="reset-button" @click="resetGame">
      {{ winner || isDraw ? 'New Game' : 'Reset Game' }}
    </button>
  </div>
</template>

<style scoped>
.game-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  padding: 2rem;
  background: linear-gradient(to bottom right, rgba(37, 99, 235, 0.1), rgba(249, 250, 251, 1));
}

.game-title {
  font-size: 3rem;
  font-weight: 700;
  color: #2563EB;
  margin-bottom: 2rem;
  text-align: center;
  text-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.status-display {
  font-size: 1.5rem;
  font-weight: 600;
  padding: 1rem 2rem;
  margin-bottom: 2rem;
  border-radius: 12px;
  background: #ffffff;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease;
  min-width: 300px;
  text-align: center;
}

.status-playing {
  color: #111827;
  border: 2px solid #2563EB;
}

.status-winner {
  color: #F59E0B;
  border: 2px solid #F59E0B;
  animation: pulse 1s ease-in-out infinite;
}

.status-draw {
  color: #6B7280;
  border: 2px solid #6B7280;
}

@keyframes pulse {
  0%, 100% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.05);
  }
}

.game-board {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1rem;
  margin-bottom: 2rem;
  padding: 1.5rem;
  background: #ffffff;
  border-radius: 16px;
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.15);
}

.cell {
  width: 100px;
  height: 100px;
  font-size: 3rem;
  font-weight: 700;
  border: none;
  border-radius: 12px;
  background: #f9fafb;
  color: #111827;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  display: flex;
  align-items: center;
  justify-content: center;
}

.cell-empty:hover:not(:disabled) {
  background: #e5e7eb;
  transform: translateY(-2px);
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.15);
}

.cell-x {
  color: #2563EB;
  background: rgba(37, 99, 235, 0.1);
}

.cell-o {
  color: #F59E0B;
  background: rgba(245, 158, 11, 0.1);
}

.cell-disabled {
  cursor: not-allowed;
}

.cell:active:not(:disabled) {
  transform: scale(0.95);
}

.reset-button {
  padding: 1rem 3rem;
  font-size: 1.125rem;
  font-weight: 600;
  color: #ffffff;
  background: #2563EB;
  border: none;
  border-radius: 12px;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 4px 6px rgba(37, 99, 235, 0.3);
}

.reset-button:hover {
  background: #1d4ed8;
  transform: translateY(-2px);
  box-shadow: 0 6px 12px rgba(37, 99, 235, 0.4);
}

.reset-button:active {
  transform: scale(0.95);
}

/* Responsive Design */
@media (max-width: 768px) {
  .game-title {
    font-size: 2rem;
  }

  .status-display {
    font-size: 1.25rem;
    min-width: 250px;
    padding: 0.75rem 1.5rem;
  }

  .cell {
    width: 80px;
    height: 80px;
    font-size: 2.5rem;
  }

  .game-board {
    gap: 0.75rem;
    padding: 1rem;
  }

  .reset-button {
    padding: 0.875rem 2rem;
    font-size: 1rem;
  }
}

@media (max-width: 480px) {
  .game-container {
    padding: 1rem;
  }

  .game-title {
    font-size: 1.75rem;
    margin-bottom: 1.5rem;
  }

  .status-display {
    font-size: 1rem;
    min-width: 200px;
    padding: 0.5rem 1rem;
    margin-bottom: 1.5rem;
  }

  .cell {
    width: 70px;
    height: 70px;
    font-size: 2rem;
  }

  .game-board {
    gap: 0.5rem;
    padding: 0.75rem;
  }

  .reset-button {
    padding: 0.75rem 1.5rem;
    font-size: 0.875rem;
  }
}
</style>
