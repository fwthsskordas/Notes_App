<script setup>

import { ref } from "vue";
const showModal = ref(false);
const newNote = ref("");
const errorMes = ref("");
const notes = ref([]);
let color = ref(null);
function getRandomColor() {
 return color.value = "hsl(" + Math.random() * 360 + ", 100%, 75%)";
}

function showTheModal() {
  showModal.value = true;
}

function closeTheModal() {
  showModal.value = false;
  newNote.value = "";
}

function createNote() {
  if (newNote.value.length < 10) {
    return errorMes.value = "Note Need 10 characters or More!";
  }
    notes.value.push({
      id: Math.floor(Math.random() * 100000),
      text: newNote.value,
      date: new Date(),
      backgroundColor: getRandomColor()
    });
    showModal.value = false;
  newNote.value = "";
  errorMes.value = "";
}
</script>


<template>
<main>
  <div class="overlay" v-if="showModal">
    <div class="modal">
      <textarea v-model.trim="newNote" name="note" id="note" cols="30" rows="10"></textarea>
      <p v-if="errorMes"> {{ errorMes }} </p>
      <button @click="createNote" > Add Note </button>
      <button class="close"  @click="closeTheModal"> Close </button>
    </div>
  </div>
  <div class="container">
    <header>
      <h1>Notes</h1>
      <button @click="showTheModal">+</button>
    </header>
    <div class="cards-container">
      <div v-for="note in notes" :key="note.id " class="card" :style="{backgroundColor: note.backgroundColor}">
        <p class="main-text"> {{note.text}} </p>
        <p class="date"> {{note.date.toLocaleDateString("en")}} </p>
      </div>
    </div>
  </div>
</main>


</template>



<style scoped>
main{
  height: 100vh;
  width: 100vw;
  background-color: rgb(34, 34, 34);
}

.container{
  max-width: 1000px;
  padding: 10px;
  margin: 0 auto;
}

header{
  display: flex;
  justify-content: space-between;
  align-items: center;
}


h1{
  font-weight: bold;
  margin-bottom: 25px;
  font-size: 65px;
}

header button{
  border: none;
  padding: 10px;
  width: 50px;
  cursor: pointer;
  height: 50px;
  background-color: rgb(38, 189, 126);
  border-radius: 100%;
  font-size: 25px;
  color: rgb(88, 86, 86);
  cursor: pointer;
}


.card{
  width: 180px;
  height: 225px;
  background-color: blueviolet;
  border-radius: 8%;
  display: flex;
  padding: 10px;
  flex-direction: column;
  justify-content: space-between;
  margin-right: 20px;
  margin-bottom: 20px;
  color: black;
}


.date{
  font-size: 12px;
  font-weight: bold;
}

.cards-container {
  display: flex;
  flex-wrap: wrap;
}

.overlay {
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: rgba(0,0,0,0.5);
  z-index: 10;
  display: flex;
  align-items: center;
  justify-content: center;
}

.modal{
  width: 550px;
  background-color: white;
  border-radius: 10px;
  padding: 20px;
  position: relative;
  display: flex;
  flex-direction: column;
}

.modal button {
  padding: 10px 20px;
  font-size: 20px;
  width: 100%;
  background-color: blueviolet;
  border: none;
  color: white;
  cursor: pointer;
  margin-top: 20px;
  border-radius: 10px;
}

.modal .close {
  background-color: brown;
}

.modal textarea {
  font-family:sans-serif;
  font-weight: bold;
  font-size: 15px;
}
.modal p{
  color: brown;
}
</style>