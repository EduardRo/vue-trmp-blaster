<!-- src/App.vue -->

<template>
  <div @keydown="handleKeyPress" tabindex="0">
    <GameBoard
      :matrix="matrix"
      :isPlayerAt="isPlayerAt"
      :filteredBombs="filteredBombs"
    />
    <div>
      <p>Player Position: {{ playerPosition.x }}, {{ playerPosition.y }}</p>
      <p>Bombs: {{ bombs.length }}</p>
    </div>
  </div>
</template>

<script>
import { defineComponent } from "vue";
import GameBoard from "./components/GameBoard.vue";

export default defineComponent({
  data() {
    return {
      playerPosition: { x: 0, y: 0 },
      bombs: [],
      matrix: this.createMatrix(10, 10),
    };
  },
  methods: {
    handleKeyPress(event) {
      switch (event.key) {
        case "ArrowUp":
          this.movePlayer("up");
          break;
        case "ArrowDown":
          this.movePlayer("down");
          break;
        case "ArrowLeft":
          this.movePlayer("left");
          break;
        case "ArrowRight":
          this.movePlayer("right");
          break;
        case " ":
          this.placeBomb();
          break;
      }
    },
    movePlayer(direction) {
      switch (direction) {
        case "up":
          this.playerPosition.y = Math.max(this.playerPosition.y - 1, 0);
          break;
        case "down":
          this.playerPosition.y = Math.min(
            this.playerPosition.y + 1,
            this.matrix.length - 1
          );
          break;
        case "left":
          this.playerPosition.x = Math.max(this.playerPosition.x - 1, 0);
          break;
        case "right":
          this.playerPosition.x = Math.min(
            this.playerPosition.x + 1,
            this.matrix[0].length - 1
          );
          break;
      }
    },
    placeBomb() {
      this.bombs.push({ x: this.playerPosition.x, y: this.playerPosition.y });
    },
    createMatrix(rows, cols) {
      const matrix = [];
      for (let i = 0; i < rows; i++) {
        const row = [];
        for (let j = 0; j < cols; j++) {
          row.push({ x: j, y: i });
        }
        matrix.push(row);
      }
      return matrix;
    },
    isPlayerAt(x, y) {
      return this.playerPosition.x === x && this.playerPosition.y === y;
    },
    filteredBombs(x, y) {
      return this.bombs.filter((bomb) => bomb.x === x && bomb.y === y);
    },
  },
  mounted() {
    // Enable keyboard events on the entire document
    document.addEventListener("keydown", this.handleKeyPress);
  },
  beforeUnmount() {
    // Remove event listener when component is destroyed to avoid memory leaks
    document.removeEventListener("keydown", this.handleKeyPress);
  },
  components: {
    GameBoard,
  },
});
</script>

<style>
/* Add global styles if needed */
</style>
