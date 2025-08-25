<script>
import NotesList from "./components/NotesList.vue";
import NoteDialog from "./components/NoteDialog.vue";
import { ref } from "vue";

export default {
  name: "App",
  components: {
    NotesList,
    NoteDialog,
  },
  setup() {
    const isAddingNote = ref(false);
    const notes = ref(JSON.parse(localStorage.getItem("notes")) ?? []);

    function toggleAddingNote() {
      isAddingNote.value = !isAddingNote.value;
    }

    function addNote({ title, content }) {
      notes.value.push({ id: notes.value.length + 1, title, content });
      localStorage.setItem("notes", JSON.stringify(notes.value));
      isAddingNote.value = false;
    }

    return { isAddingNote, notes, addNote, toggleAddingNote };
  },
};
</script>

<template>
  <div id="app">
    <button
      @click="toggleAddingNote"
      class="add-note"
      :class="{ rotated: isAddingNote }"
    >
      +
    </button>
    <NoteDialog
      v-if="isAddingNote"
      @add-note="
        (note) => {
          addNote({ title: note.title, content: note.content });
        }
      "
      @cancel="toggleAddingNote"
    />
    <NotesList :notes="notes" />
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
