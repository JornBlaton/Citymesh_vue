<template>

</template>

<script setup>

async function fetchrooms() {
  try {
    const response = await fetch('https://jokes-api-by-api-ninja.p.rapidapi.com/v1/jokes');
    const jokes = await response.json();
  } catch (error) {
    console.error(error);
  }
}
</script>