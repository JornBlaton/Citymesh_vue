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

const state = reactive({
    data: null,
})

const form = reactive({
    date: null,
    amount: 0
});

function submit() {
    fetchrooms();
    console.log(state.data)
}

async function fetchrooms() {
    try { 
        await fetch(`http://localhost:8000/api/meetingtimes?date=${form.date}&amount=${form.amount}`, {
        method: 'GET',
        headers: {
            'Content-Type': 'application/json',
        },
        }).then(res => {
            state.data = res.json();
            return res;
        })
    } catch (error) {
        console.log(error)
    }
}

</script>
