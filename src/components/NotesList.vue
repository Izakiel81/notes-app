<script setup >
  import NoteItem from './NoteItem.vue';
  import { ref } from 'vue';
  
  const notes = ref([{ id: 0, title: 'Sample Note', content: 'This is a sample note.' }]);

</script>

<template>
  <div>
   <button @click="$emit('add-note')" class="add-note">+</button> 
    <div v-for="note in notes" :key="note.id"> 
      <NoteItem :note="note" />
    </div> 
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
