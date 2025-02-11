<template>
    <TestRef/>
</template>

<script lang="ts">
import TestRef from './components/TestRef.vue';
export default {
    name: 'App',
    components: {
        TestRef
    }
}
</script>

<style scoped>
.app {
    background-color: #ddd;
    box-shadow: 0 0 10px;
    border-radius: 10px;
    padding: 20px;
}
</style>