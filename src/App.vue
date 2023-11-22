<!-- src/App.vue -->

<template>
  <div>
    <div class="game-board">
      <div v-for="(row, rowIndex) in matrix" :key="rowIndex" class="board-row">
        <div
          v-for="(cell, cellIndex) in row"
          :key="cellIndex"
          class="board-cell"
        >
          <!-- Display player at the current position -->
          <div v-if="isPlayerAt(cell.x, cell.y)" class="player"></div>
          <!-- Display bombs at their positions -->
          <div
            v-for="(bomb, bombIndex) in filteredBombs(cell.x, cell.y)"
            :key="'bomb-' + bombIndex"
            class="bomb"
          ></div>
        </div>
      </div>
    </div>
    <div>
      <button @click="movePlayer('up')">Up</button>
    </div>
    <div>
      <button @click="movePlayer('left')">Left</button>
      <button @click="placeBomb">Place Bomb</button>
      <button @click="movePlayer('right')">Right</button>
    </div>
    <div>
      <button @click="movePlayer('down')">Down</button>
    </div>
    <div>
      <p>Player Position: {{ playerPosition.x }}, {{ playerPosition.y }}</p>
      <p>Bombs: {{ bombs.length }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      playerPosition: { x: 0, y: 0 },
      bombs: [],
      matrix: this.createMatrix(10, 10), // Adjust the size of the matrix as needed
    };
  },
  methods: {
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
};
</script>

<style>
.game-board {
  display: flex;
  flex-direction: column;
  /*display: grid; */
  grid-template-columns: repeat(10, 100px); /* Each column is 100 pixels wide */
  grid-template-rows: repeat(10, 100px); /* Each row is 100 pixels tall */
  grid-gap: 2px;
}

.board-row {
  display: flex;
}

.board-cell {
  width: 40px;
  height: 40px;
  border: 1px solid #ccc;
  position: relative;
}

.player {
  width: 100%;
  height: 100%;
  background-color: #00f; /* Blue color for the player */
}

.bomb {
  width: 100%;
  height: 100%;
  background-color: #f00; /* Red color for bombs */
}
</style>
