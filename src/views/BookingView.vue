<template>
  <header class="m-5">
    <button
      @click="$emit('changeView', 'HomeView')"
      class="p-1 border-2 border-black rounded-md"
    >
      Back
    </button>
  </header>
  <div class="flex flex-row">
    <div class="m-10">
      <div id="bookingcontainer">
        <div v-for="item in props.meetingdata" :key="item.id" class="border-2 border-black rounded-md mb-2 p-1">
          <p>Room_id: {{ item.room }}</p>
          <p>Booked for: {{ item.person }}</p>
          <p>Starting time:{{ item.timestamp_start }}</p>
          <p>Ending time: {{ item.timestamp_end }}</p>
        </div>
      </div>
      <div id="roomcontainer">
        <h2>Select room:</h2>
        <button
          v-for="item in props.rooms"
          @click="(form.room = item.id), console.log(form.room)"
          :key="item.id"
          class="border-2 border-black rounded-md mr-2 p-1">
          {{ item.name }}
        </button>
      </div>
    </div>
    <form @submit.prevent="submit" class="flex flex-col mt-3 ml-5 mr-5">
      <label for="email">Email:</label>
      <input
        type="email"
        id="email"
        name="email"
        v-model="form.email"
        class="border-2 border-black rounded-md"
      />
      <label for="start">Start Time:</label>
      <input
        type="time"
        id="start"
        name="start"
        v-model="form.start"
        class="border-2 border-black rounded-md"
      />
      <label for="end">End Time:</label>
      <input
        type="time"
        id="end"
        name="end"
        v-model="form.end"
        class="border-2 border-black rounded-md"
      />
      <save-button />
    </form>
    <table class="h-[500px] border-separate border border-slate-400">
        <tr class="">
          <td>06:00</td>
          <td>12:30</td>
        </tr>
        <tr>
          <td>06:30</td>
          <td>13:00</td>
        </tr>
        <tr>
          <td>07:00</td>
          <td>13:30</td>
        </tr>
        <tr>
          <td>07:30</td>
          <td>14:00</td>
        </tr>
        <tr>
          <td>08:00</td>
          <td>14:30</td>
        </tr>
        <tr>
          <td>08:30</td>
          <td>15:00</td>
        </tr>
        <tr>
          <td>09:30</td>
          <td>15:30</td>
        </tr>
        <tr>
          <td>10:00</td>
          <td>16:00</td>
        </tr>
        <tr>
          <td>10:30</td>
          <td>16:30</td>
        </tr>
        <tr>
          <td>11:00</td>
          <td>17:00</td>
        </tr>
        <tr>
          <td>11:30</td>
          <td>17:30</td>
        </tr>
        <tr>
          <td>12:00</td>
          <td>18:00</td>
        </tr>
      </table>
  </div>
  
</template>

<script setup>
import { defineProps, reactive } from "vue";
import SaveButton from "@/components/SubmitButton.vue";

const props = defineProps(["meetingdata", "rooms"]);

const form = reactive({
  curdate: props.meetingdata[0].selected_date,
  room: null,
  email: null,
  start: null,
  end: null,
});

function submit() {
  createBooking();
}

async function createBooking() {
  try {
    await fetch(`http://localhost:8000/api/meetings`, {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: { form },
    }).then((res) => {
      return res.json();
    });
  } catch (error) {
    console.log(error);
  }
}
</script>
