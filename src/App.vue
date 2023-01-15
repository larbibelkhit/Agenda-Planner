<script setup>
import Todos from './components/Todos.vue';
import DayNotes from './components/DayNotes.vue';
import University from './components/University.vue';
import Work from './components/Work.vue';
import Header from './components/Header.vue';
import Footer from './components/Footer.vue';
</script>

<template>
  <div>
    <div class="row mb-5 pb-1">
      <div class="col"><Header /></div>
    </div>
    <div class="row ml-1 mr-1">
      <div class="col-7"><DayNotes /></div>
      <div class="col"><Todos /></div>
    </div>
    <div class="row ml-1 mr-1">
      <div class="col"><University /></div>
      <div class="col"><Work /></div>
    </div>
    <div class="row mt-3">
      <div class="col"><Footer /></div>
    </div>
  </div>
</template>

<style>
</style>
