<script setup>
import NoteItem from "./NoteItem.vue";
import { defineProps } from "vue";

defineProps({ notes: Array });
</script>

<template>
  <div v-for="note in notes" :key="note.id">
    <NoteItem :note="note" />
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
