<script setup>
import { ref } from 'vue';

const myArray = ref([])
const month = ref('')
const input_content = ref('')
const input_category = ref(null)

const addGroceries = () =>{
  if(input_content.value.trim() === '' || input_category.value == nul){
    return
  }
  myArray.value.push({
    content: input_content.value,
    category: input_category.value,
  })

  input_content.value = ''
  input_category.value = null
}


</script>

<template>
  <main class="app">

    <section class="greeting">
      <h2 class="title">
        Welcome back, for what month are we buying?, <input type="text" placeholder="Enter Month" v-model="month">
      </h2>
    </section>

    <section class="create-Groceries">
      <h3>ENTER GROCERIES NEEDED THIS MONTH</h3>
      <form @submit.prevent = "addGroceries">
        <h4>What do we need?</h4>
        <input type="text" placeholder="e.g., Milk" v-model="input_content"/>


      <h4>Pick a Category</h4>
      <div class="options">
        <label>
          <input type="radio" name="category" value="foods" v-model="input_category">
          <span class="bubble foods"></span>
        </label>
        <label>
          <input type="radio" name="category" value="snacks" v-model="input_category">
          <span class="bubble snacks"></span>
        </label>
      </div>
      <input type="submit" value="Add Groceries"/>
      </form>

    </section>

    <section class="Groceries-list">


    </section>


  </main>

</template>
