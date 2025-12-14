<script setup>

import CardsList from './components/CardsList.vue';
import Header from './components/Header.vue';




</script>
<template>

    <div class="w-4/5 bg-white m-auto bg-white  rounded-xl shadow-2xl mt-14">
        <Header />


        <div class="p-10">
            <h2 class="text-3xl font-bold mb-8">Все Кроссовки</h2>
            <CardsList />
        </div>
    </div>



</template>

<style scoped></style>
