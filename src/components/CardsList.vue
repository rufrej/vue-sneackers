<script setup>
import Card from './Card.vue';


</script>

<template>
    <div class="grid grid-cols-4 gap-5">
        <Card title="Кроссовки мужские Nike HyperPyper" imageUrl="/sneakers/sneakers-2.jpg" :price="880"
            :isAdded="false" :isFavorite="false" />
    </div>
</template>