<script setup>
import { ref } from 'vue'
const props = defineProps({
  sticks: Number
})

const sticks = ref(props.sticks);
const userRemoveAmt = ref(0);
defineExpose({sticks,userRemoveAmt});

const clean_matchstick = '/src/assets/clean_matchstick.png';

const emit = defineEmits(['removeEvent']);
function handleRemove() {
    if(userRemoveAmt.value <= 0) return;
    emit('removeEvent',  userRemoveAmt.value);
    sticks.value = sticks.value - userRemoveAmt.value;
    userRemoveAmt.value = 0;
}
</script>

<template>
  <div class="card nimheap" v-if="sticks >= 1">
    <div class="container">
        <div class="row">
            <div class="col-1">
                <h2 style="color:white;">{{sticks}}</h2>
            </div>
            <div class="col-9">
                <img class="stick" v-for="index in sticks" :src="clean_matchstick">
            </div>
            <div class="col-2">
                <div class="row">
                    <input type="range" v-model="userRemoveAmt" min="0" :max="sticks">
                </div>
                <div class="row">
                    <button class="btn btn-danger" @click="handleRemove()">Remove {{ userRemoveAmt }} Sticks</button>
                </div>
            </div>
        </div>
    </div>
  </div>
</template>

<style scoped>
.nimheap {
    background-color: black;
    margin: 0;
    padding: 0;
    border: white;
    border-style: solid;
    border-radius: 5px;
}
.stick {
    height: 100px;
}
#rmvForm {
    justify-content: center;
}
</style>
