<template>
    <h1>computed的基本使用</h1>
    <div class="test-computed">
        <div class="basic">
            姓：<input type="text" v-model="firstName"> <br> <br>
            名：<input type="text" v-model="lastName"> <br> <br>
            全名：{{ fullName }}
            <div class="operations">
                <button @click="changeFullName">改全名</button>
            </div>
        </div>
    </div>
</template>

<script setup lang="ts">
import { ref, reactive, computed } from 'vue';
//computed的基本使用
let firstName = ref('')
let lastName = ref('')
// let fullName = computed(() => {
//     return firstName.value.slice(0, 1).toUpperCase() + firstName.value.slice(1) + ' ' + lastName.value
// })
//带setter的写法
let fullName = computed({
    get() {
        return firstName.value.slice(0, 1).toUpperCase() + firstName.value.slice(1) + ' ' + lastName.value
    },
    set(val) {
        console.log('new fullname is:' + val);
        const [str1, str2] = val.split(' ')
        firstName.value = str1
        lastName.value = str2
    }
})
function changeFullName() {
    fullName.value = 'li si'
}
</script>

<style scoped>
.basic {
    background-color: #e9e9e9;
    box-shadow: 0 0 10px;
    border-radius: 10px;
    padding: 20px;
}

.operations {
    margin-top: 15px;
}

.operations button {
    margin-right: 5px;
}
</style>