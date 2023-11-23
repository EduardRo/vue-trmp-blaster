<!-- src/components/BombGame.vue -->

<template>
  <div class="bomb-game"></div>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  // You can add any component-specific methods or logic here
});
</script>

<style scoped>
.bomb-game {
  width: 50px;
  height: 50px;
  background-color: rgb(120, 13, 99); /* Red color for bombs */
  position: absolute;
}
</style>
