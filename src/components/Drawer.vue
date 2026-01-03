<script setup>
import { computed } from 'vue';
import CartItem from './CartItem.vue';
import CartListItem from './CartListItem.vue';
import DrawerHeader from './DrawerHeader.vue';
import InfoBlock from './InfoBlock.vue';

const emit = defineEmits(['createOrder'])

const props = defineProps({
    totalPrice: Number,
    vatPrice: Number,
    isCreatingOrder: Boolean

})

const buttonDisable = computed(() => props.isCreatingOrder ? true : props.totalPrice ? false : true)
</script>

<template>

    <div class="fixed top-0 left-0 h-full w-full bg-black z-10 opacity-70"></div>

    <div class="bg-white w-96 h-full fixed right-0 top-0 z-20 p-8">

        <DrawerHeader />

        <div v-if="!totalPrice" class="flex h-full items-center">
            <InfoBlock title="Корзина пуста" description="Добавьте хотя бы одну пару кроссовок, что-бы сделать заказ"
                -image-url="/package-icon.png" />
        </div>


        <div v-else>
            <CartListItem />
            <div class="flex flex-col gap-4 mt-7">

                <div class="flex gap-2 ">
                    <span>Итого :</span>
                    <div class="flex-1 border-b border-slate-200"></div>
                    <b>{{ Math.floor(totalPrice) }} BYN</b>
                </div>

                <div class="flex gap-2 ">
                    <span>Налог 5%:</span>
                    <div class="flex-1 border-b border-slate-200"></div>
                    <b>{{ vatPrice }} BYN</b>
                </div>
                <button type="button" :disabled="buttonDisable" @click="() => emit('createOrder')"
                    class="mt-4 cursor-pointer bg-lime-500 w-full rounded-xl py-3 text-white disabled:bg-slate-400 hover:bg-lime-600 transition active:bg-lime-700">
                    Оформить заказ
                </button>
            </div>
        </div>

    </div>


</template>