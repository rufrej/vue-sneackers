<script setup>

import Card from './Card.vue';

defineProps({
    items: Array
})

const emit = defineEmits(['addToFavorite', 'addToDrawer'])

</script>

<template>
    <div class="grid grid-cols-4 gap-5">
        <Card v-for="item in items" :key="item.id" :id="item.id" :title="item.title" :imageUrl="item.imageUrl"
            :price="item.price" :isAdded="item.isAdded" :onClickFavorite="() => emit('addToFavorite', item)"
            :onClickAdd="() => emit('addToDrawer', item)" :isFavorite="item.isFavorite" />
    </div>
</template>