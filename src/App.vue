<script setup>

import { onMounted, provide, reactive, ref, watch } from 'vue';
import axios from 'axios';
import CardsList from './components/CardsList.vue';
import Drawer from './components/Drawer.vue';
import Header from './components/Header.vue';

const items = ref([])

const filters = reactive({
    sortBy: 'title',
    searchQuery: '',
})


const onChangeSelect = (event) => {
    filters.sortBy = event.target.value
}

const onChangeSearchInput = (event) => {
    filters.searchQuery = event.target.value
}

const fetchItems = async () => {
    try {

        const params = {
            sortBy: filters.sortBy
        }

        if (filters.searchQuery) {
            params.title = `*${filters.searchQuery}*`
        }
        const { data } = await axios.get('https://e2a9ee0d546589a2.mokky.dev/items',
            { params }
        )
        items.value = data.map((object) => ({
            ...object,
            isFavorite: false,
            favoriteId: null,
            isAdded: false,
        }))
    } catch (err) {
        console.log(err)
    }

}

const fetchFavorites = async () => {
    try {
        const { data: favorites } = await axios.get('https://e2a9ee0d546589a2.mokky.dev/favorites',)

        items.value = items.value.map(item => {
            const favorite = favorites.find(favorite => favorite.parentId === item.id)

            if (!favorite) {
                return item
            }

            return {
                ...item,
                isFavorite: true,
                favoriteId: favorite.id,
            }
        })
    } catch (err) {
        console.log(err)
    }

}

const addToFavorite = async (item) => {


    try {
        if (!item.isFavorite) {
            const object = {
                parentId: item.id,
            }

            item.isFavorite = true

            const { data } = await axios.post('https://e2a9ee0d546589a2.mokky.dev/favorites', object)

            item.favoriteId = data.id
            console.log(data)
        } else {

            item.isFavorite = false
            axios.delete(`https://e2a9ee0d546589a2.mokky.dev/favorites/${item.favoriteId}`)
            item.favoriteId = null

        }

    } catch (err) {
        console.log(err)
    }


}

onMounted(async () => {
    await fetchItems()
    await fetchFavorites()

})

watch(filters, fetchItems)
provide('addToFavorite', addToFavorite)

</script>
<template>
    <!-- <Drawer /> -->

    <div class="w-4/5 bg-white m-auto  rounded-xl shadow-2xl mt-14">
        <Header />


        <div class="p-10">
            <div class="flex justify-between items-center mb-8">
                <h2 class="text-3xl font-bold">Все Кроссовки</h2>

                <div class="flex gap-4">

                    <select @change="onChangeSelect" name="" id="" class="py-2 px-3 border rounded-md outline-none">
                        <option value="name">По названию</option>
                        <option value="price">По цене(дешевые)</option>
                        <option value="-price">По цене(дорогие)</option>

                    </select>

                    <div class="relative">
                        <img class="absolute left-5 top-3" src="/search.svg" alt="search">
                        <input @input="onChangeSearchInput" type="text" placeholder="Поиск"
                            class="border border-gray-200 rounded-md py-2 pl-11 pr-4 outline-none focus:border-gray-800">
                    </div>

                </div>
            </div>
            <CardsList :items="items" @addToFavorite="addToFavorite" />
        </div>
    </div>



</template>

<style scoped></style>
