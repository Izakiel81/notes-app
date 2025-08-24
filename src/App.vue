<script>
import NotesList from './components/NotesList.vue';
import NoteAddDialog from './components/NoteAddDialog.vue';
import { ref } from 'vue';

export default {
  name: 'App', 
  components: {
    NotesList,
    NoteAddDialog
  },
  setup() {

    const isAddingNote = ref(false);
    const newNoteTitle = ref('');
    const newNoteContent = ref('');

    function toggleAddingNote() {
      isAddingNote.value = !isAddingNote.value;
    }

    return { isAddingNote, newNoteTitle, newNoteContent, toggleAddingNote};

  }
}
</script>

<template>
  <div id="app">
    <button 
     @click="toggleAddingNote" 
     class="add-note"
     :class="{'rotated': isAddingNote}">
       +
     </button> 
      <NoteAddDialog 
	v-if="isAddingNote"
	@add-note="toggleAddingNote" 
	@cancel="toggleAddingNote"
	/>
    <NotesList/>
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
.rotated {
  transform: rotate(45deg);
}
.add-note {
  width: 40px;
  height: 40px;
  display: block;
  padding: 10px;
  margin-bottom: 10px;
  background-color: #28a745;
  color: white;
  border: none;
  border-radius: 50%; 
  cursor: pointer;
  transition: transform 0.2s ease-in-out;
}

</style>
