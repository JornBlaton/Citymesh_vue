<template>
  <div>
    <button @click="$emit('changeView', 'HomeView')">Back</button>

    <div id="roomcontainer">
      <button
        v-for="item in props.rooms"
        @click="(form.room = item.id), console.log(form.room)"
        :key="item.id"
      >
        {{ item.name }}
      </button>
    </div>

    <table>
      <tr>
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

    <form @submit.prevent="submit" class="flex flex-col mt-3 ml-5 mr-5">
      <label for="email">Email:</label>
      <input type="email" id="email" name="email" v-model="form.email" />
      <label for="start">Start Time:</label>
      <input type="time" id="start" name="start" v-model="form.start" />
      <label for="end">End Time:</label>
      <input type="time" id="end" name="end" v-model="form.end" />
      <save-button />
    </form>
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
