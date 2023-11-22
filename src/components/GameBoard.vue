<!-- src/components/GameBoard.vue -->

<template>
  <div class="game-board">
    <div v-for="(row, rowIndex) in matrix" :key="rowIndex" class="board-row">
      <div v-for="(cell, cellIndex) in row" :key="cellIndex" class="board-cell">
        <PlayerGame v-if="isPlayerAt(cell.x, cell.y)" />
        <BombGame
          v-for="(bomb, bombIndex) in filteredBombs(cell.x, cell.y)"
          :key="'bomb-' + bombIndex"
        />
      </div>
    </div>
  </div>
</template>

<script>
import { defineComponent } from "vue";
import PlayerGame from "./PlayerGame.vue";
import BombGame from "./BombGame.vue";

export default defineComponent({
  props: ["matrix", "isPlayerAt", "filteredBombs"],
  components: {
    PlayerGame,
    BombGame,
  },
});
</script>

<style scoped>
.game-board {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.board-row {
  display: flex;
}

.board-cell {
  width: 50px;
  height: 50px;
  border: 1px solid #ccc;
  position: relative;
}
</style>
