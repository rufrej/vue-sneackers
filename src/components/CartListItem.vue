<script setup>
import { inject } from 'vue';
import CartItem from './CartItem.vue';

const { drawer, removeFromDrawer } = inject('drawer')



</script>

<template>

    <div class="flex flex-col gap-4 justify-beetween">
        <CartItem v-for="item in drawer" :key="item.id" :title="item.title" :price="item.price"
            :image-url="item.imageUrl" @on-click-remove="() => removeFromDrawer(item)" />
    </div>
</template>