<script setup>
import Header from './components/Header.vue';
import MainPage from './components/MainPage.vue';
import Footer from './components/Footer.vue';
import Button from '@/volt/Button.vue'
</script>

<template>
  <div class="h-screen bg-gradient-to-b from-[var(--p-primary-50)] to-[var(--p-primary-400)] flex flex-col overflow-hidden">
    <Header></Header>
    <MainPage />
    <Footer />
  </div>

</template>

<style scoped>

</style>
