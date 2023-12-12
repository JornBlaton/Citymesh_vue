<template>
   <component :is="tabs[currentTab]" @changeView="changeView"/>
</template>

<script setup>
import { ref } from 'vue'
import HomeView from '@/views/HomeView.vue'
import BookingView from '@/views/BookingView.vue'
import RoomView from '@/views/RoomView.vue'


const currentTab = ref('HomeView')

const tabs = {
  HomeView,
  BookingView,
  RoomView
}

function changeView(page) {
  currentTab.value = page
}
</script>