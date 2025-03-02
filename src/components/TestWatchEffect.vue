<template>
    <div class="basic">
        <h2>watchEffect</h2>
        <h3>体重：{{ weight }}</h3>
        <h3>身高：{{ height }}</h3>
        <button @click="fatter">增重</button>
        <button @click="taller">增高</button>
    </div>
</template>

<script setup lang="ts">
import { ref, reactive, computed, watch, watchEffect } from 'vue';

let weight = ref(100)
let height = ref(150)

//不用watchEffect的写法
// watch(([weight, height]), (newVal) => {
//     let [newWeight, newHeight] = newVal
//     if (newWeight > 150 || newHeight > 190) {
//         console.log("warning...........");
//     }
// })
function fatter() {
    weight.value += 10
}
function taller() {
    height.value += 10
}
//使用watchEffect
watchEffect(() => {
    if (weight.value > 150 || height.value > 190) {
        console.log("warning...........");
    }
})


</script>

<style scoped>
.basic {
    background-color: #e9e9e9;
    box-shadow: 0 0 10px;
    border-radius: 10px;
    padding: 20px;
}
</style>