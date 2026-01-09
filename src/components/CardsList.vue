<script setup>

import Card from './Card.vue';

defineProps({
    items: Array,
    isFavorites: Boolean,
})

const emit = defineEmits(['addToFavorite', 'addToDrawer'])


</script>

<template>
    <div class="grid grid-cols-1  gap-5 sm:grid-cols-2 md:grid-cols-4" v-auto-animate>
        <Card v-for="item in items" :key="item.id" :id="item.id" :title="item.title" :imageUrl="item.imageUrl"
            :price="item.price" :onClickFavorite="isFavorites ? null : () => emit('addToFavorite', item)"
            :onClickAdd="isFavorites ? null : () => emit('addToDrawer', item)" :isFavorite="item.isFavorite"
            :isAdded="item.isAdded" />
    </div>
</template>