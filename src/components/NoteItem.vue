<script setup>
import { defineProps } from 'vue';
defineProps({
  note: {
    id: Number,
    title: String,
    content: String,
  } 
});
</script>	
<template>
  <div class="note-item">
    <h3>{{ note.title }}</h3>
    <p>{{ note.content }}</p>
  </div>
</template>

<style scoped>
.note-item {
  padding: 10px;
  border-bottom: 1px solid #eee; 
}
</style>
