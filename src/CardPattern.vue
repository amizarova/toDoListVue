<script setup>
import { defineProps } from 'vue';
defineProps({
  isImportant: {
    default: false,
    type: Boolean,
    required: true,
  }, 
});
</script>

<template>
<div class="card" :class="{important: isImportant}">

</div>
</template>

<style>
.card {
    width: 150px;
    height: 200px;
    border-radius: 15px;
    background-color: rgb(132, 0, 255);
    display: flex;
    justify-content: center;
    align-items: center;
    border: solid 1px white;
    padding: 10px;
    background-image: url("assets/notImportantCat.jpg");
    background-size: cover;
}
.important {
    background-color: rgb(211, 165, 255);
    background-image: url("assets/importantCat.webp");
    border: solid 1px rgb(0, 0, 0);
}
</style>