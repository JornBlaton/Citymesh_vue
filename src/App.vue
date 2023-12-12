<template>
   <component :is="tabs[currentTab]" @changeView="changeView"/>
</template>

<script setup>
import { ref, reactive } from 'vue'
import HomeView from '@/views/HomeView.vue'
import BookingView from '@/views/BookingView.vue'
import RoomView from '@/views/RoomView.vue'


const currentTab = ref('HomeView')

const tabs = {
  HomeView,
  BookingView,
  RoomView
}

const state = reactive({
    data: null,
})

function changeView(page, data) {
  currentTab.value = page
  state.data = data
  console.log(data)
}
</script>