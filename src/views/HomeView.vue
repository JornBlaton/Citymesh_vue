<template>
  <div>
    <form @submit.prevent="submit" class="flex flex-col mt-3 ml-5 mr-5">
      <label for="date">Select Date:</label>
      <input type="date" id="date" name="date" v-model="form.date" />
      <label for="amount">Amount of Participants:</label>
      <input type="number" id="amount" name="amount" v-model="form.amount" />
      <save-button />
    </form>
  </div>
</template>

<script setup>
import SaveButton from "@/components/SubmitButton.vue";
import { reactive, defineEmits } from "vue";

const emit = defineEmits(["changeView"]);

const state = reactive({
  data: null,
  rooms: null,
});

const form = reactive({
  date: null,
  amount: 0,
});

function submit() {
  fetchCheckRooms();
  fetchrooms();
}

async function fetchrooms() {
  try {
    await fetch(
      `http://localhost:8000/api/meetingtimes?date=${form.date}&amount=${form.amount}`,
      {
        method: "GET",
        headers: {
          "Content-Type": "application/json",
        },
      }
    )
      .then((res) => {
        return res.json();
      })
      .then((resdata) => {
        state.data = resdata;
        emit("changeView", "BookingView", state.data, state.rooms);
        console.log(resdata);
      });
  } catch (error) {
    console.log(error);
  }
}

async function fetchCheckRooms() {
  try {
    await fetch(`http://localhost:8000/api/roomsize?amount=${form.amount}`, {
      method: "GET",
      headers: {
        "Content-Type": "application/json",
      },
    })
      .then((res) => {
        return res.json();
      })
      .then((resdata) => {
        console.log(resdata);
        state.rooms = resdata;
      });
  } catch (error) {
    console.log(error);
  }
}
</script>
