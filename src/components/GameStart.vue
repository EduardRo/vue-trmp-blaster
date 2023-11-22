<!-- src/components/Game.vue -->
<template>
  <div ref="game"></div>
</template>

<script>
import Phaser from "phaser";

export default {
  name: "GameStart",
  mounted() {
    const config = {
      type: Phaser.AUTO,
      width: 800,
      height: 600,
      scene: {
        preload: this.preload,
        create: this.create,
        update: this.update,
      },
    };

    this.game = new Phaser.Game(config);
  },
  methods: {
    preload() {
      // Load assets (sprites, tiles, etc.)
    },
    create() {
      // Set up the initial state of the game
    },
    update() {
      // Main game loop, update game state
    },
  },
};
</script>

<style scoped>
/* Add your custom styles here */
</style>
