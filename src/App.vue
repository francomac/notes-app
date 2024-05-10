<script setup>
import { ref } from "vue";

const showModal = ref(false);
const newNote = ref("");
const notes = ref([]);
const errorMessage = ref("");

const addNote = () => {
  if (!newNote.value && newNote.value.length === 0) {
    errorMessage.value = "Please enter a note";
    return;
  }
  notes.value.push({
    id: Math.floor(Math.random() * 100000),
    text: newNote.value,
    date: new Date().toLocaleDateString(),
    color: `rgb(${Math.floor(Math.random() * 256)}, ${Math.floor(
      Math.random() * 256
    )}, ${Math.floor(Math.random() * 256)})`,
  });

  newNote.value = "";
  errorMessage.value = "";
  showModal.value = false;
};
</script>

<template>
  <main>
    <div v-if="showModal" class="overlay">
      <div class="modal">
        <textarea
          @keyup.esc="addNote"
          v-model.trim="newNote"
          name="notes"
          id="notes"
          cols="30"
          rows="10"
        ></textarea>
        <p v-if="errorMessage">{{ errorMessage }}</p>
        <button @click="addNote">Add Note</button>
        <button @click="showModal = false" class="close">Close</button>
      </div>
    </div>
    <div class="container">
      <header>
        <h1>Notes</h1>
        <button @click="showModal = true">+</button>
      </header>
      <div class="cards-container">
        <div
          v-for="note in notes"
          :key="note.id"
          class="card"
          :style="{ backgroundColor: note.color }"
        >
          <p class="main-text">{{ note.text }}</p>
          <p class="date">{{ note.date }}</p>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
main {
  width: 100vw;
  height: 100vh;
  background-color: white;
  color: black;
}
.cards-container {
  display: flex;
  flex-wrap: wrap;
}
.container {
  max-width: 800px;
  padding: 20px;
  margin: 0 auto;
}
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
h1 {
  font-weight: bold;
  margin-bottom: 25px;
  font-size: 5rem;
}
header button {
  background-color: rgp(21, 20, 20);
  border: none;
  border-radius: 50px;
  font-size: 2rem;
  cursor: pointer;
  padding: 5px;
  width: 50px;
  height: 50px;
}
.card {
  width: 220px;
  height: 220px;
  background-color: rgb(237, 182, 44);
  padding: 10px;
  border-radius: 15px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: flex-start;
  margin: 0 20px 20px 0;
  overflow: scroll;
}

.main-text {
  color: white;
  font-size: 1.2rem;
  line-height: 1.5;
  text-align: left;
  font-weight: 300;
}

.date {
  color: white;
  font-size: 0.8rem;
  font-weight: bold;
}

.overlay {
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: rgb(0, 0, 0, 0.5);
  z-index: 10;
  display: flex;
  align-items: center;
  justify-content: center;
}
.modal {
  padding: 30px;
  background-color: white;
  border-radius: 10px;
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 750px;
}
.modal textarea {
  width: 100%;
  background-color: #f0f0f0;
  height: 200px;
  font-size: 20px;
  padding: 10px;
  margin-bottom: 20px;
}
.modal p {
  color: red;
  margin-bottom: 20px;
}
.modal button {
  padding: 10px 20px;
  font-size: 20px;
  width: 100%;
  background-color: blueviolet;
  cursor: pointer;
}
.modal .close {
  background-color: red;
  margin-top: 8px;
}
</style>