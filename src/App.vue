<script setup>
import {ref} from 'vue'

let show_modal = ref(false);
let new_note = ref('');
let notes = ref([]);
let show_note = ref(false);
let showwarning = ref(false);

function Getbg(){
  return "hsl(" + Math.random() * 360 + " , 100%, 75%)";
}

const addnote= () => {

    if( new_note.value.length > 10){
      showwarning.value = false;
      notes.value.push({
      text: new_note.value,
      date: new Date(),
      bg: Getbg()
      })
      show_modal.value = false;
      show_note.value = true;
      new_note.value = '';
    }else{
      showwarning.value = true;
    }
  
}

const deleteNote = (index) => {
  notes.value.splice(index, 1);
  
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
        <p class="warning" v-if="showwarning">Note should contain more than 10 characters</p>
        <textarea name="note" id="note" cols="30" rows="10" v-model="new_note" @keyup.enter="addnote" placeholder="Enter a new note">{{ new_note }}</textarea>
        <button class="add" @click="addnote">Add Note</button>
        <button class="close" @click="toggle_modal">close</button>
      </div>
    </div>
    <div class="container">
      <header>
        <h1>Notes </h1>
        <button class="header-button" @click="toggle_modal" >+</button>
      </header>
      <div class="cards-container">
        <div class="card" v-for="(note, index) in notes" :key="index" :style="{backgroundColor: note.bg}" >
          <button class="delete" @click="deleteNote(index)" >x</button>
          <p class="main-text">{{ note.text }}</p>
          <p class="date">{{ note.date.toLocaleDateString("en-Us") }}</p>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
main{
  height: 100vh;
  width: 100vw;
  background-color: rgb(255, 255, 255);
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
  border-bottom: solid rgb(65, 59, 59);
  margin-bottom: 10px;
}
h1{
  font-weight: bold;
  margin-bottom: 25px;
  font-size: 3em;

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
  background-color: rgb(93, 184, 116);
  color: white;
  cursor: pointer;
}
.close{
  padding: 10px;
  margin-top: 10px;
  border-radius: 5px;
  border: none;
  background-color: rgb(63, 103, 139);
  color: white;
  cursor: pointer;
}
.card{
  width: 225px;
  height: 225px;
  background-color: black;
  color: rgb(39, 39, 39);
  padding: 10px;
  display: flex;
  flex-direction: column;
  border-radius: 15px;
  justify-content: space-between;
  margin-right: 20px;
  margin-bottom: 20px;
}
.delete{
  position: absolute;
  width: 25px;
  border: none;
  border-radius: 1000px;
  background-color: black;
  color: white;
  align-self: flex-end;
  cursor: pointer;
  margin-bottom: 10px;
}
.main-text{
  font-size: 20px;
  margin-left: 10px;
  margin-top: 10px;
  font-weight: bold;
  white-space:normal; word-break: break-all
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
.warning{
  text-align: center;
  font-weight: bold;
  color: red;
}
</style>