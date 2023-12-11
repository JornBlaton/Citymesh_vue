<template>
    <div>
        <form @submit.prevent="submit" class="flex flex-col mt-3 ml-5 mr-5">
            <label for="id">Select Date:</label>
            <input type="date" id="date" name="date" v-model="form.date">
            <label for="amount">Amount of Participants:</label>
            <input type="number" id="amount" name="amount" v-model="form.amount">
            <save-button/>
        </form>
    </div>
</template>

<script setup>
import SaveButton from "@/components/SubmitButton.vue";
import {reactive} from "vue";

const form = reactive({
    date: null,
    amount: 0
});

function submit() {
    console.log(form)
}
</script>
