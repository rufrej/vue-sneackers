<script setup>
defineProps({
    title: String,
    imageUrl: String,
    price: Number,


})

</script>

<template>

    <div
        class="relative border border-slate-100 rounded-3xl p-8 cursor-pointer transition hover:-translate-y-2 hover:shadow-xl">
        <img class="absolute top-5 left-5" src="/like-2.svg" alt="like-2">
        <img :src="imageUrl" alt="Sneakers">
        <p class="mt-2">{{ title }}</p>


        <div class="flex justify-between mt-5">
            <div class="flex flex-column">
                <b class="text-slate-400">Цена: </b>
                <span>{{ price }} BYN</span>
            </div>
            <img src="/plus.svg" alt="plus">
        </div>
    </div>
</template>