<script setup>
import { computed, ref } from 'vue'

const props = defineProps({
  gameBoard: Array
})

const Heaps = ref(props.NimHeaps);
</script>

<template>
  <div class="nimgame">
    
  </div>
</template>

<style scoped>
.nimgame {
    width: 80%;
    height:100%;
}
</style>
