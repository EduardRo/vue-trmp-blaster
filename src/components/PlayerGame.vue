<!-- src/components/PlayerGame.vue -->

<template>
  <div class="player-game"></div>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  props: ["position"],
  watch: {
    position(newValue) {
      this.updatePlayerPosition(newValue);
    },
  },
  mounted() {
    this.updatePlayerPosition(this.position);
  },
  methods: {
    updatePlayerPosition(position) {
      const playerElement = this.$el;
      playerElement.style.left = `${position.x * 50}px`;
      playerElement.style.top = `${position.y * 50}px`;
    },
  },
});
</script>

<style scoped>
.player-game {
  width: 50px;
  height: 50px;
  background-color: #00f; /* Blue color for the player */
  position: absolute;
  transition: left 0.3s, top 0.3s;
}
</style>
