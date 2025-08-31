<script setup>
import NoteItem from "./NoteItem.vue";
import NoteDialog from "./NoteDialog.vue";
import { ref } from "vue";

const isAddingNote = ref(false);
const notes = ref(JSON.parse(localStorage.getItem("notes")) ?? []);

function deleteNote(id) {
  if (notes.value.length === 1) {
    localStorage.removeItem("notes");
    notes.value = [];
    return;
  }
  notes.value = notes.value.filter((note) => note.id !== id);
  localStorage.setItem("notes", JSON.stringify(notes.value));
}
function editNote(editedNote) {
  const index = notes.value.findIndex((note) => note.id === editedNote.id);
  if (index !== -1) {
    notes.value[index] = editedNote;
    localStorage.setItem("notes", JSON.stringify(notes.value));
  }
}
function toggleAddingNote() {
  isAddingNote.value = !isAddingNote.value;
}
function addNote({ title, content }) {
  notes.value.push({ id: notes.value.length + 1, title, content });
  localStorage.setItem("notes", JSON.stringify(notes.value));
}
</script>
<template>
  <button
    @click="toggleAddingNote"
    class="add-note"
    :class="{ rotated: isAddingNote }"
    title="Add Note"
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
  <div class="notes-container" v-for="note in notes" :key="note.id">
    <NoteItem
      :note="note"
      @delete-note="(note) => deleteNote(note.id)"
      @edit-note="(note) => editNote(note)"
    />
  </div>
</template>

<style scoped>
.notes-container {
  display: flex;
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
