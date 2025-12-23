<script setup>

import Card from './Card.vue';

defineProps({
    items: Array
})



const onCliclAdd = () => {
    alert('Add')
}

const emit = defineEmits(['addToFavorite'])

</script>

<template>
    <div class="grid grid-cols-4 gap-5">
        <Card v-for="item in items" :key="item.id" :id="item.id" :title="item.title" :imageUrl="item.imageUrl"
            :price="item.price" :isAdded="false" :onClickFavorite="() => emit('addToFavorite', item)"
            :isFavorite="item.isFavorite" :onClickAdd="onCliclAdd" />
    </div>
</template>