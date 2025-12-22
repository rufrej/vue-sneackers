<script setup>
defineProps({
    title: String,
    imageUrl: String,
    price: Number,
    isFavorite: Boolean,
    isAdded: Boolean,
    onClickAdd: Function,
    onClickFavorite: Function,
})

</script>

<template>

    <div
        class="relative border border-slate-100 rounded-3xl p-8 cursor-pointer transition hover:-translate-y-2 hover:shadow-xl">
        <img class="absolute top-5 left-5" :src="!isFavorite ? '/like-1.svg' : '/like-2.svg'" alt="like-2"
            @click="onClickFavorite">



        <img :src="imageUrl" alt="Sneakers">
        <p class="mt-2">{{ title }}</p>


        <div class="flex justify-between mt-5">
            <div class="flex flex-column">
                <b class="text-slate-400">Цена: </b>
                <span>{{ Math.floor(price / 30) }} BYN</span>
            </div>
            <img @click="onClickAdd" :src="!isAdded ? '/plus.svg' : '/checked.svg'" alt="plus">
        </div>
    </div>
</template>