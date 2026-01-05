<script setup>
import CardsList from '@/components/CardsList.vue';
import axios from 'axios';
import { onMounted, ref } from 'vue';


const favorites = ref([])
onMounted(async () => {
    try {
        const { data } = await axios.get('https://e2a9ee0d546589a2.mokky.dev/favorites?_relations=items')

        favorites.value = data.map(obj => obj.item)
    } catch (err) {
        console.error(err)
    }
})
</script>

<template>

    <h2 class="text-3xl font-bold">Мои закладки</h2>

    <CardsList :items="favorites" is-favorites />
</template>