<script setup>

import CardsList from './components/CardsList.vue';
import Drawer from './components/Drawer.vue';
import Header from './components/Header.vue';

</script>
<template>
    <!-- <Drawer /> -->

    <div class="w-4/5 bg-white m-auto  rounded-xl shadow-2xl mt-14">
        <Header />


        <div class="p-10">
            <div class="flex justify-between items-center mb-8">
                <h2 class="text-3xl font-bold">Все Кроссовки</h2>

                <div class="flex gap-4">

                    <select name="" id="" class="py-2 px-3 border rounded-md outline-none">
                        <option value="">По названию</option>
                        <option value="">По цене(дешевые)</option>
                        <option value="">По цене(дорогие)</option>

                    </select>

                    <div class="relative">
                        <img class="absolute left-5 top-3" src="/search.svg" alt="search">
                        <input type="text" placeholder="Поиск"
                            class="border border-gray-200 rounded-md py-2 pl-11 pr-4 outline-none focus:border-gray-800">
                    </div>

                </div>
            </div>
            <CardsList />
        </div>
    </div>



</template>

<style scoped></style>
