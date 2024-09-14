<script setup>
import { ref } from 'vue';

const month = ref('')

</script>

<template>
  <main class="app">

    <section class="greeting">
      <h2 class="title">
        Welcome back, for what month are we buying?, <input type="text" placeholder="Enter Month" v-model="month">
      </h2>
    </section>

    <section class="create-Groceries">


    </section>

    <section class="Groceries-list">


    </section>


  </main>

</template>
