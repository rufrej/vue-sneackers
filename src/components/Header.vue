<script setup>

defineProps({
    totalPrice: Number

})
const emit = defineEmits(['OpenDrawer'])

</script>

<template>

    <header class="flex flex-col justify-between border-b border-slate-100 px-10 py-8 md:flex-row">

        <router-link to="/">

            <div class="flex items-center gap-4">
                <img class="w-10" src="/logo.png" alt="Logo">
                <div>
                    <h2 class="text-xl font-bold uppercase">Vue Sneakers</h2>
                    <p class=" hidden text-slate-400 md:block">Магазин лучшич коссовок</p>
                </div>
            </div>

        </router-link>

        <nav>
            <ul class="flex items-center gap-10 text-sm md:text-xl">
                <li @click="() => emit('OpenDrawer')"
                    class="flex items-center gap-3 text-gray-500 cursor-pointer hover:text-black">
                    <img src="/cart.svg" alt="Cart">
                    <b>{{ totalPrice }}BYN</b>
                </li>
                <router-link to="/favorites">
                    <li class="flex items-center gap-3 text-gray-500 cursor-pointer hover:text-black">


                        <img src="/heart.svg" alt="Cart">
                        <b>Избранное</b>


                    </li>
                </router-link>
                <li class="flex items-center gap-3 text-gray-500 cursor-pointer hover:text-black">
                    <img src="/profile.svg" alt="Cart">
                    <b>Профиль</b>
                </li>
            </ul>
        </nav>

    </header>
</template>