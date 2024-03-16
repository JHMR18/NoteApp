<script setup>
import {ref} from 'vue'

let show_modal = ref(false);
let new_note = ref('');
let notes = ref([]);
let show_note = ref(false);
let date = ref(Date().toString());


const addnote= () => {
  notes.value.push(new_note.value)
  show_modal.value = false;
  show_note.value = true;
  new_note.value = '';
  
}


const toggle_modal = () => {
  show_modal.value = !show_modal.value;
  console.log('modal triggered')
}


</script>


<template>
  <main>
    <div class="overlay" v-if="show_modal" >
      <div class="modal">
        <textarea name="note" id="note" cols="30" rows="10" v-model="new_note" placeholder="Enter a new note">{{ new_note }}</textarea>
        <button class="add" @click="addnote">Add Note</button>
        <button class="close" @click="toggle_modal">close</button>
      </div>
    </div>
    <div class="container">
      <header>
        <h1>Notes</h1>
        <button class="header-button" @click="toggle_modal" >+</button>
      </header>
      <div class="cards-container">
        <div class="card" v-for="(note) in notes">
          <p class="main-text">{{ note }}</p>
          <p class="date">{{ date }}</p>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
main{
  height: 100vh;
  width: 100vw;
  background-color: aquamarine;
}
.container{
  max-width: 1000px;
  padding: 10px;
  margin: 0 auto;
}
.cards-container{
  display: flex;
  flex-wrap: wrap;
}
header{
  display: flex;
  justify-content: space-between;
  align-items: center;
  color: black;
}
h1{
  font-weight: bold;
  margin-bottom: 25px;
  font-size: 50px;

}
.header-button{
  border: none;
  padding: 10px;
  width: 50px;
  height: 50px;
  cursor: pointer;
  background-color: rgb(0, 0, 0);
  border-radius: 1000px;
  color: white;
  font-size: 20px;
}

.add{
  padding: 10px;
  margin-top: 5px;
  border-radius: 5px;
  border: none;
  background-color: black;
  color: white;
  cursor: pointer;
}
.close{
  padding: 10px;
  margin-top: 10px;
  border-radius: 5px;
  border: none;
  background-color: black;
  color: white;
  cursor: pointer;
}
.card{
  width: 225px;
  height: 225px;
  background-color: black;
  color: white;
  padding: 10px;
  display: flex;
  flex-direction: column;
  border-radius: 15px;
  justify-content: space-between;
  margin-right: 20px;
  margin-bottom: 20px;
}
.main-text{
  font-size: 20px;
  margin-left: 10px;
  margin-top: 10px;
}
.date{
  font-size: 12px;
  margin-left: 10px;
  margin-top: 10px;
  font-weight: bold;
}
.overlay{
  position:absolute;
  width: 100%;
  height: 100%;
  background-color: rgb(0,0,0,0.77);
  z-index: 10;
  display: flex;
  align-items: center;
  justify-content: center;
}
.modal{
  width: 750px;
  background-color: white;
  border-radius: 10px;
  padding: 30px;
  display: flex;
  flex-direction: column;
}
textarea{
  border-radius: 10px;
  font-size: larger;
  font-weight: bold;
}
</style>