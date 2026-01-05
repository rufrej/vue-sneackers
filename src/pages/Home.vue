<script setup>
import { inject, onMounted, reactive, ref, watch } from 'vue';
import CardsList from '../components/CardsList.vue';
import axios from 'axios';
import debounce from 'lodash.debounce'

const { drawer, addToDrawer, removeFromDrawer } = inject('drawer')
const items = ref([])
const filters = reactive({
    sortBy: 'title',
    searchQuery: '',
})



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
            favorite_id: null,
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
            const favorite = favorites.find(favorite => favorite.item_id === item.id)

            if (!favorite) {
                return item
            }

            return {
                ...item,
                isFavorite: true,
                favorite_id: favorite.id,
            }
        })
    } catch (err) {
        console.log(err)
    }

}



const onChangeSelect = (event) => {
    filters.sortBy = event.target.value
}

const onChangeSearchInput = debounce((event) => {
    filters.searchQuery = event.target.value
}, 300)

const addToFavorite = async (item) => {


    try {
        if (!item.isFavorite) {
            console.warn(item)
            const object = {

                item_id: item.id,
            }

            item.isFavorite = true

            const { data } = await axios.post('https://e2a9ee0d546589a2.mokky.dev/favorites', object)

            item.favorite_id = data.id
            console.log(data)
        } else {

            item.isFavorite = false
            axios.delete(`https://e2a9ee0d546589a2.mokky.dev/favorites/${item.favorite_id}`)
            item.favorite_id = null

        }

    } catch (err) {
        console.log(err)
    }


}

const onClickAddPlus = (item) => {
    if (!item.isAdded) {
        addToDrawer(item)
    } else {
        removeFromDrawer(item)
    }
}

onMounted(async () => {
    const locarDrawer = localStorage.getItem('drawer')
    drawer.value = locarDrawer ? JSON.parse(locarDrawer) : [];


    await fetchItems()
    await fetchFavorites()

    items.value = items.value.map((item) => ({
        ...item,
        isAdded: drawer.value.some((cartItem) => cartItem.id === item.id)
    }))

})

watch(drawer, () => {
    items.value = items.value.map((item) => ({
        ...item,
        isAdded: false
    }))
})



watch(filters, fetchItems)

</script>

<template>
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
    <div class="mt-10">
        <CardsList :items="items" @add-to-favorite="addToFavorite" @add-to-drawer="onClickAddPlus" />

    </div>
</template>