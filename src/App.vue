<template>
  <component
    :is="tabs[currentTab]"
    @changeView="changeView"
    :meetingdata="state.data"
    :rooms="state.rooms"
  />
</template>

<script setup>
import { ref, reactive } from "vue";
import HomeView from "@/views/HomeView.vue";
import BookingView from "@/views/BookingView.vue";
import RoomView from "@/views/RoomView.vue";

const currentTab = ref("HomeView");

const tabs = {
  HomeView,
  BookingView,
  RoomView,
};

const state = reactive({
  data: null,
  rooms: null
});

function changeView(page, data, rooms) {
  currentTab.value = page;
  state.data = data;
  state.rooms = rooms
}
</script>
