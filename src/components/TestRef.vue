<template>
    <!-- Ref的基本使用 -->
    <h1>Ref的基本使用</h1>
    <div class="test-ref">
        <div class="basic">
            <h2>我的名字是：{{ name }}</h2>
            <h2>我的年龄是：{{ age }}</h2>
        </div>

        <div class="operations">
            <button @click="changeName">改名</button>
            <button @click="changeAge">改年龄</button>
            <button @click="showTel">展示号码</button>
        </div>
    </div>
    <hr>
    <!-- Reactive的基本使用 -->
    <h1>Reactive的基本使用</h1>
    <div class="test-reactive">
        <div class="basic">
            <h2>房子的价格是：{{ house.price }}</h2>
            <h2>房子的位置是：{{ house.position }}</h2>
        </div>
        <div class="operations">
            <button @click="addHousePrice">涨价！</button>
            <button @click="addHeatForFirstGame">给鸣潮加点热度！</button>
        </div>
        <ul>
            <li v-for="game in games" :key="game.name">
                游戏名：{{ game.name }} | 热度：{{ game.heat }}
            </li>
        </ul>
    </div>
    <hr>
    <!-- toRefs和toRef -->
    <h1>toRefs和toRef</h1>
    <div class="test-toRefs">
        <div class="basic">
            <h2>银行账户是：{{ bank.account }}</h2>
            <h2>账户余额是：{{ bank.balance }}</h2>
            <h2>账户余额(toRef)是：{{ balance_ref }}</h2>
        </div>
        <div class="operations">
            <button @click="changeAccount">改名</button>
            <button @click="changeBalance">充值</button>
        </div>
    </div>
</template>

<script setup lang="ts" name="pp">
import { ref, reactive, computed, toRefs, toRef } from 'vue';

// ref的基本使用
let name = ref('James')
let age = ref(25)
let tel = '56789'

function changeName() {
    name.value = name.value + '1'
}

function changeAge() {
    age.value++
}

function showTel() {
    alert('我的号码是：' + tel)
}

// reactive的基本使用
let house = reactive({ price: 8888888, position: 'Shanghai' })
let games = reactive([{ name: '鸣潮', heat: 666666 }, { name: '荒野大镖客', heat: 999999 }, { name: '最后生还者2', heat: 333333 }])

function addHousePrice() {
    house.price += 100000
}

function addHeatForFirstGame() {
    games[0].heat += 1000
}

//toRefs和toRef
let bank = reactive({account: 'abc', balance: 500})
let {account, balance} = toRefs(bank) //toRefs会把响应式对象里的每个属性解构成一个个单独的响应式数据,toRef只结构某一个属性
let balance_ref = toRef(bank, 'balance')

function changeAccount() {
    account.value += 'c'
}

function changeBalance() {
    balance.value += 100
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

ul {
    padding: 0;
}
</style>