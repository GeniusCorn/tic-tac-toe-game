<script setup lang="ts">
const board: string[][] = $ref([
  ['', '', ''],
  ['', '', ''],
  ['', '', '']
])

type Player = 'O' | 'X'

let player: Player = 'O'

function move(x: number, y: number): void {
  if (board[x][y] !== '') return
  if (winner !== null) return

  board[x][y] = player

  player = player === 'O' ? 'X' : 'O'
}

function resetBoard(): void {
  for (let i = 0; i < board.length; i += 1) {
    for (let j = 0; j < board[i].length; j += 1) {
      board[i][j] = ''
    }
  }

  player = 'O'
}

const lines: number[][] = [
  [0, 1, 2],
  [3, 4, 5],
  [6, 7, 8],
  [0, 3, 6],
  [1, 4, 7],
  [2, 5, 8],
  [0, 4, 8],
  [2, 4, 6]
]

function calculateWinner(board: string[]): string | null {
  for (let i = 0; i < lines.length; i += 1) {
    const [a, b, c] = lines[i]

    if (board[a] !== '' && board[a] === board[b] && board[a] === board[c])
      return board[a]
  }
  return null
}

function calculateEmpty(board: string[]): boolean {
  for (let i = 0; i < board.length; i += 1) {
    if (board[i] === '') return true
  }

  return false
}

const winner: string | null = $computed(() => calculateWinner(board.flat()))
const isEmpty: boolean = $computed(() => calculateEmpty(board.flat()))

const statusMessage = $computed(() => {
  if (winner === null && !isEmpty) return `It's a draw!`

  if (winner === null) return `It's ${player}'s turn.`
  else return `${winner} has won!`
})
</script>

<template>
  <div grid grid-cols-3>
    <div v-for="(x, xIndex) in 3" :key="xIndex">
      <div
        v-for="(y, yIndex) in 3"
        :key="yIndex"
        border
        w-10
        h-10
        flex="~"
        justify-center
        items-center
        @click="move(xIndex, yIndex)"
      >
        <div>
          {{ board[xIndex][yIndex] }}
        </div>
      </div>
    </div>
  </div>

  <div>
    {{ statusMessage }}
  </div>

  <div flex="~">
    <div
      bg-green-200
      p-2
      text-sm
      rounded-lg
      hover:opacity-50
      cursor-pointer
      transition
      duration-200
      ease-in-out
      @click="resetBoard"
    >
      Reset
    </div>
  </div>
</template>

<style scoped></style>
