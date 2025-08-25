<script setup>
import NoteItem from "./NoteItem.vue";
import { defineProps, toRefs } from "vue";

const props = defineProps({ notes: Array });
const { notes } = toRefs(props);

function deleteNote(id) {
  localStorage.setItem(
    "notes",
    JSON.stringify(notes.value.filter((note) => note.id !== id))
  );
}
</script>

<template>
  <div v-for="note in notes" :key="note.id">
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
