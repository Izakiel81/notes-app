<script>
import NotesList from './components/NotesList.vue';
import { ref } from 'vue';

export default {
  name: 'App', 
  components: {
    NotesList
  },
  setup() {

    const isAddingNote = ref(false);

    function toggleAddingNote() {
      isAddingNote.value = !isAddingNote.value;
    }

    return { isAddingNote, toggleAddingNote};

  }
}
</script>

<template>
  <div id="app">
    <button @click="toggleAddingNote" class="add-note">+</button> 
    <form v-if="isAddingNote">
	<input/>	
	<textarea/>	
	<button >Add Note</button>
    </form>
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
}

</style>
