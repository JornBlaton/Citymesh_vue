<template>
    <div>
        <button @click="$emit('changeView', 'HomeView')">Back</button>
        <p>{{ props.meetingdata }}</p>
    </div>
</template>

<script setup>
import { defineProps } from 'vue'

const props = defineProps(['meetingdata'])
</script>