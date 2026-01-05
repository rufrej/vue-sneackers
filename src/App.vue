<script setup>

import { computed, provide, ref, watch } from 'vue';


import Drawer from './components/Drawer.vue';
import Header from './components/Header.vue';


const drawer = ref([])


const drawerOpen = ref(false)

const totalPrice = computed(
    () => Math.floor(drawer.value.reduce((acc, item) => acc + item.price, 0) / 30)
)

const vatPrice = computed(
    () => Math.round(totalPrice.value * 5) / 100
)


const openDrawer = () => {
    drawerOpen.value = true
}
const closeDrawer = () => {
    drawerOpen.value = false
}

const addToDrawer = (item) => {

    drawer.value.push(item)
    item.isAdded = true

}
const removeFromDrawer = (item) => {
    drawer.value.splice(drawer.value.indexOf(item), 1)
    item.isAdded = false
}



watch(drawer, () => {
    localStorage.setItem('drawer', JSON.stringify(drawer.value))
},
    { deep: true })

provide('drawer', {
    drawer,
    closeDrawer,
    openDrawer,
    addToDrawer,
    removeFromDrawer,

})

</script>
<template>
    <Drawer v-if="drawerOpen" :total-price="totalPrice" :vat-price="vatPrice" />

    <div class="w-4/5 bg-white m-auto  rounded-xl shadow-2xl mt-14">
        <Header :total-price="totalPrice" @open-drawer="openDrawer" />
        <div class="p-10">
            <router-view></router-view>
        </div>
    </div>
</template>
<style scoped></style>
