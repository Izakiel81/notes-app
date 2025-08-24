<script setup>
  
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
  function cancel() {
    emit('cancel');
    newNoteTitle.value = '';
    newNoteContent.value = ''; 
  }

</script>
<template>
   <span class="overlay"></span>
   <div class="dialog">
    <form @submit.prevent="addNote" class="note-form"> 
     <label>Title:</label>
     <input v-model="newNoteTitle" />	

     <label>Note:</label>
     <textarea v-model="newNoteContent" />	
      
     <div class="buttons">
       <button id="add">Add Note</button>
       <button id="cancel" @click="cancel">Cancel</button>
     </div>
    </form>
   </div>
</template>
<style scoped>
.overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  z-index: 999;
}
.dialog {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background: white;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  z-index: 1000;

  width: 400px;
  max-width: 90%;
  box-sizing: border-box;
}
.note-form {
  display: flex;
  flex-direction: column;
}
.note-form label {
  margin-bottom: 5px;
  font-weight: 600;
}
.note-form input, .note-form textarea {
  outline: none;
  width: 100%;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
  margin-bottom: 15px;
  transition: border-color 0.3s, box-shadow 0.3s;
}
.note-form input:focus, .note-form textarea:focus {
  border-color: #007BFF;
  box-shadow: 0 0 5px rgba(0, 123, 255, 0.5);
}
.note-form textarea {
  resize: vertical;
  min-height: 100px;
  max-height: 200px;
}
.buttons {
  display: flex;
  justify-content: flex-end;
  gap: 10px;
}
.note-form button {
  color: white;
  border: none;
  padding: 10px;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s, transform 0.1s;
}
.note-form button:hover {
  opacity: 0.9;
}
.note-form button:active {
  transform: scale(0.98);
}
.note-form #add {
  background-color: #28a745;
}
.note-form #cancel {
  background-color: #dc3545;
}
</style>

