<template>
    <h1>ref标签的使用</h1>
    <div class="basic">
        <h2 ref="title">Me</h2>
        <Person ref="human" />
        <button @click="show">show</button>
    </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue';
import Person from './Person.vue';

let title = ref()
let human = ref()
function show() {
    console.log(human.value);

}
</script>

<style scoped>
.basic {
    background-color: #e9e9e9;
    box-shadow: 0 0 10px;
    border-radius: 10px;
    padding: 20px;
}
</style>