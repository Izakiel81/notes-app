<script setup>
import NoteItem from "./NoteItem.vue";
import { defineProps, toRefs, ref } from "vue";

const props = defineProps({ notes: Array });
const { notes } = toRefs(props);
const localNotes = ref(notes.value);
function deleteNote(id) {
  localNotes.value = localNotes.value.filter((note) => note.id !== id);
  localStorage.setItem("notes", JSON.stringify(localNotes.value));
}

</script>
<template>
  <div v-for="note in localNotes" :key="note.id">
    <NoteItem :note="note" @delete-note="(note) => deleteNote(note.id)" />
  </div>
</template>

<style scoped>
.note-list {
  max-width: 600px;
  margin: 20px auto;
  border: 1px solid #ccc;
  border-radius: 5px;
  background-color: #f9f9f9;
  padding: 10px;
}
</style>
