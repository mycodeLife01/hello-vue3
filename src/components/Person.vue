<template>
    <div class="person">
        <h1>我的名字是：{{ name }}</h1>
        <h1>我的年龄是：{{ age }}</h1>
    </div>

    <div class="operations">
        <button @click="changeName">改名</button>
        <button @click="changeAge">改年龄</button>
        <button @click="showTel">展示号码</button>
    </div>
    
</template>

<script setup lang="ts" name="pp">
import { ref, reactive, computed } from 'vue';

let name = ref('James')
let age = ref(25)
let tel = ref('56789')

function changeName() {
    name.value = name.value + '1'
}

function changeAge() {
    age.value++
}

function showTel() {
    alert('我的号码是：' + tel.value)
}
</script>

<style scoped>
.person {
    background-color: #ddd;
    box-shadow: 0 0 10px;
    border-radius: 10px;
    padding: 20px;
}
.operations {
    margin-top: 15px;
}
.operations button{
    margin-right: 5px;
}
</style>