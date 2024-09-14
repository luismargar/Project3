<script setup>
import {ref, onMounted, watch} from 'vue';

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
    done: false,
  })

  input_content.value = ''
  input_category.value = null
}

const removegroceries = (x) =>{
  myArray.value = myArray.value.filter(Element => Element !== x)
}

onMounted ( () =>{
  month.value = localStorage.getItem('month') || ''
  myArray.value = JSON.parse(localStorage.getItem('myArray')) || []
})

watch(month, (newVal) =>{
  localStorage.setItem('month', newVal)
})

watch(myArray, (newVal) =>{
  localStorage.setItem('myArray', JSON.stringify(newVal))
}, {deep: true})

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
      <div class="list">
        <div v-for="x in myArray" :class="`groceries-item ${x.done ? 'done' : 'not-done'}`" :key="x">

          <label>
            <input type="checkbox" v-model="x.done"/>
            <span :class="`bubble ${x.category}`"></span>
          </label>

          <div class="groceries-content">
            <input type="text" v-model="x.content"/>
          </div>

          <div class="actions">
            <button class="delete" @click="removegroceries(x)">Delete</button>
          </div>
        </div>
      </div>
    </section>
  </main>
</template>
