<script setup>
import { defineProps, defineEmits, toRefs, ref } from "vue";
import NoteDialog from "./NoteDialog.vue";
const props = defineProps({
  note: {
    id: Number,
    title: String,
    content: String,
  },
});
const { note } = toRefs(props);
const isEditing = ref(false);
const isDeleting = ref(false);
const emit = defineEmits(["edit-note", "delete-note"]);
</script>
<template>
  <NoteDialog
    v-if="isEditing"
    :note="note"
    @edit-note="(note) => emit('edit-note', note)"
    @cancel="() => (isEditing = false)"
  />
  <NoteDialog
    v-if="isDeleting"
    :note="note"
    @delete-note="(note) => emit('delete-note', note)"
    @cancel="() => (isDeleting = false)"
  >
    <div>
      <h3>Are you sure you want to delete this note?</h3>
      <p>
        <strong>{{ note.title }}</strong>
      </p>
      <p>{{ note.content }}</p>
      <div class="buttons">
        <button id="delete" @click="$emit('delete-note', note)">Delete</button>
        <button id="cancel" @click="() => (isDeleting = false)">Cancel</button>
      </div>
    </div>
  </NoteDialog>
  <div class="note-item">
    <h3>{{ note.title }}</h3>
    <p>{{ note.content }}</p>
    <div class="icons">
      <button @click="isEditing = true" title="Edit Note" id="edit">
        Edit
      </button>
      <button @click="isDeleting = true" title="Delte Note" id="delete">
        Delete
      </button>
    </div>
  </div>
</template>

<style scoped>
.note-item {
  padding: 10px;
  border-bottom: 1px solid #eee;
  width: 100%;
  box-sizing: border-box;
}
.icons {
  display: flex;
}
.icons button {
  cursor: pointer;

  width: 50%;
  height: 40px;
  font-size: 1.1rem;

  transition: filter 0.3s ease-in-out;
}
.icons button:hover {
  filter: brightness(0.9);
}
.icons button:active {
  filter: brightness(0.8);
}

#edit {
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
}
#delete {
  background-color: #dc3545;
  color: white;
  border: none;
  border-radius: 4px;
}
.buttons {
  display: flex;
  justify-content: flex-end;
  gap: 10px;
}
.buttons button {
  color: white;
  border: none;
  padding: 10px;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s, transform 0.1s;
}
.buttons button:hover {
  opacity: 0.9;
}
.buttons button:active {
  transform: scale(0.98);
}
.buttons #delete {
  background-color: #dc3545;
}
.buttons #cancel {
  background-color: #28a745;
}
</style>
