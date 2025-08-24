<script>
  
  import { ref, defineEmits } from 'vue';
  
  const emit = defineEmits(['add-note']);
  const newNoteTitle = ref('');
  const newNoteContent = ref('');
  
  function addNote() {
    if (!newNoteTitle.value.trim() || !newNoteContent.value.trim()) return;

    emit('add-note', {
      title:newNoteTitle.value,
      content:newNoteContent.value
    });
    newNoteTitle.value = '';
    newNoteContent.value = ''; 
  }

</script>
<template>
  <form @submit.prevent="addNote"> 
   <input v-model="newNoteTitle" />	
   <textarea v-model="newNoteContent" />	

   <button>Add Note</button>
   <button @click="cancel">Cancel</button>
  </form>
</template>
<style scoped>

</style>
