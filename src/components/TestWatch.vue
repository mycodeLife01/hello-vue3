<template>
    <div class="basic">
        <h1>Watch的基本使用</h1>
        <h2>情况一：监视Ref定义的基本类型数据</h2>
        <h3>sum: {{ count }}</h3>
        <button @click="addCount">sum+1</button>
        <hr>
        <h2>情况二：监视Ref定义的对象类型数据</h2>
        <h3>姓名：{{ person.name }}</h3>
        <h3>年龄：{{ person.age }}</h3>
        <button @click="changeName">改名</button>
        <button @click="changeAge">改年龄</button>
        <button @click="changePerson">换人</button>
        <hr>
        <h2>情况三：监视Reactive定义的对象类型数据</h2>
        <h3>书名：{{ book.title }}</h3>
        <h3>销量：{{ book.sale }}</h3>
        <button @click="changeTitle">改书名</button>
        <button @click="promote">促销</button>
        <button @click="changeBook">换书</button>
        <hr>
        <h2>情况三：监视Reactive定义的对象类型数据中的部分数据</h2>
        <h3>用户名：{{ user.name }}</h3>
        <h3>账户1：{{ user.account.account1 }}</h3>
        <h3>账户2：{{ user.account.account2 }}</h3>
        <button @click="changeUserName">改用户名</button>
        <button @click="changeAccount1">改账户一</button>
        <button @click="changeAccount2">改账户二</button>
        <button @click="changeAccount">改账户</button>
    </div>
</template>

<script setup lang="ts">
import { ref, reactive, computed, watch } from 'vue';

// watch监视ref定义的基本类型数据
let count = ref(0)
function addCount() {
    count.value++
}
const stopWatch = watch(count, (newVal, oldVal) => {
    console.log("old count:" + oldVal + ", new count:" + newVal)
    if (newVal >= 10) {
        stopWatch()
    }
})

// watch监视ref定义的对象类型的数据
let person = ref({ 'name': 'Evan', 'age': 22 })
function changeName() {
    person.value.name += '~'
}
function changeAge() {
    person.value.age++
}
function changePerson() {
    person.value = { 'name': 'zs', 'age': 19 }
}
watch(person, (newVal, oldVal) => {
    console.log("person变化了" + newVal + "-" + oldVal);
}, {
    deep: true
})

// watch监视reactive定义的对象类型数据
let book = reactive({ 'title': 'Three Body Problem', 'sale': 99999 })
function changeTitle() {
    book.title += '~'
}
function promote() {
    book.sale += 100
}
function changeBook() {
    Object.assign(book, { 'title': 'Fairy Tale', 'sale': 500000 })
}
watch(book, (newVal, oldVal) => {
    console.log(newVal, oldVal);
})

//watch监视reactive定义的对象类型数据中的部分数据
let user = reactive({
    'name': 'Jack',
    'account': {
        'account1': 'aa',
        'account2': 'bb'
    }
})
function changeUserName() {
    user.name += '~'
}
function changeAccount1() {
    user.account.account1 = 'a1'
}
function changeAccount2() {
    user.account.account2 = 'a2'
}
function changeAccount() {
    user.account = {
        'account1': 'cc',
        'account2': 'dd'
    }
}
//要监视某项数据，第一个参数一定要传函数式
// watch(() => user.name, (newVal, oldVal) => {
//     console.log('用户名发生了改变：', newVal, oldVal);
// })
//要监视对象数据的变化，使用函数式+deep，只用函数式不能检测对象数据内部数据的变化，第一个传user.account只能监测对象内部数据变化，而不能监测整体对象的变化
// watch(() => user.account, (newVal, oldVal) => {
//     console.log('账户发生了改变：', newVal, oldVal);
// }, { deep: true })
// watch(user.account, (newVal, oldVal)=>{
//     console.log('账户发生了改变：', newVal, oldVal);  
// })
//监视上述类型的组合
watch(([() => user.name, () => user.account]), (newVal, oldVal) => {
    console.log(newVal, oldVal);
}, { deep: true })
</script>

<style scoped>
.basic {
    background-color: #e9e9e9;
    box-shadow: 0 0 10px;
    border-radius: 10px;
    padding: 20px;
}
</style>