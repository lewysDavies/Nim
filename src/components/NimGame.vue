<script setup>
import { ref } from 'vue'
import NimHeap from '/src/components/NimHeap.vue'

const props = defineProps({
  heaps: Array
})

const nimHeaps = ref(props.heaps);
const userTurn = ref(true);

function removeSticks(heap, amount) {
    let newAmt = nimHeaps.value[heap] - amount;
    nimHeaps.value[heap] = newAmt;

    if(wasLastMove()) {
        alert(userTurn.value ? "Player A Wins!" : "Player B Wins!");
    } else {
        userTurn.value = !userTurn.value;
    }
}

function wasLastMove() {
    return nimHeaps.value.filter(value => value >= 1).length <= 0
}

// function handleComputersTurn() {
//     userTurn.value = false;
//     setTimeout(() => {
//         //MakeMove();
//         userTurn.value = true;
//     }, 2000);
// }
</script>

<template>
  <div class="nim-game">
    <h1>The Game of Nim...</h1>
    <p>Remove as many sticks from each pile as you wish. The one who removes the last stick from the last pile wins.</p>
    <br>
    <h2>{{ userTurn ? "Player A's Turn..." : "Player B's Turn..."}}</h2>
    <div class="col">
        <div class="row" v-for="(sticks, index) in nimHeaps">
            <NimHeap :sticks=sticks @removeEvent="(amt) => removeSticks(index, amt)"></NimHeap>
        </div>
    </div>
  </div>
</template>

<style scoped>
.nim-game {
    width: 100%;
    height:100%;
}
h1 {
    color: white;
}
p {
    color: white;
}
h2 {
    color: white;
    font-size: 42;
    text-align: left;
}
</style>
