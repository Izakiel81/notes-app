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
  <NoteDialog v-if="isEditing" :note="note" @edit-note="(note) => emit('edit-note', note)" @cancel="() => isEditing = false"/>
  <NoteDialog v-if="isDeleting" :note="note" @delete-note="(note) => emit('delete-note', note)" @cancel="() => isDeleting = false">
   <div>
      <h3>Are you sure you want to delete this note?</h3>
      <p><strong>{{ note.title }}</strong></p>
      <p>{{ note.content }}</p>
      <div class="buttons">
        <button id="delete" @click="$emit('delete-note', note)">Delete</button>
        <button id="cancel" @click="() => isDeleting = false">Cancel</button>
      </div>
   </div>
  </NoteDialog>
  <div class="note-item">
    <h3>{{ note.title }}</h3>
    <p>{{ note.content }}</p>
    <div class="icons">
      <span @click="isEditing = true">
        <svg
          fill="#000000"
          viewBox="0 0 24 24"
          version="1.2"
          baseProfile="tiny"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M21.561 5.318l-2.879-2.879c-.293-.293-.677-.439-1.061-.439-.385 0-.768.146-1.061.439l-3.56 3.561h-9c-.552 0-1 .447-1 1v13c0 .553.448 1 1 1h13c.552 0 1-.447 1-1v-9l3.561-3.561c.293-.293.439-.677.439-1.061s-.146-.767-.439-1.06zm-10.061 9.354l-2.172-2.172 6.293-6.293 2.172 2.172-6.293 6.293zm-2.561-1.339l1.756 1.728-1.695-.061-.061-1.667zm7.061 5.667h-11v-11h6l-3.18 3.18c-.293.293-.478.812-.629 1.289-.16.5-.191 1.056-.191 1.47v3.061h3.061c.414 0 1.108-.1 1.571-.29.464-.19.896-.347 1.188-.64l3.18-3.07v6zm2.5-11.328l-2.172-2.172 1.293-1.293 2.171 2.172-1.292 1.293z"
          />
        </svg>
      </span>
      <span @click="isDeleting = true">
        <svg viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path
            d="M7 4a2 2 0 0 1 2-2h6a2 2 0 0 1 2 2v2h4a1 1 0 1 1 0 2h-1.069l-.867 12.142A2 2 0 0 1 17.069 22H6.93a2 2 0 0 1-1.995-1.858L4.07 8H3a1 1 0 0 1 0-2h4V4zm2 2h6V4H9v2zM6.074 8l.857 12H17.07l.857-12H6.074zM10 10a1 1 0 0 1 1 1v6a1 1 0 1 1-2 0v-6a1 1 0 0 1 1-1zm4 0a1 1 0 0 1 1 1v6a1 1 0 1 1-2 0v-6a1 1 0 0 1 1-1z"
            fill="#0D0D0D"
          /></svg
      ></span>
    </div>
  </div>
</template>

<style scoped>
.note-item {
  padding: 10px;
  border-bottom: 1px solid #eee;
}
.icons {
  display: flex;
}
.icons span {
  margin-right: 10px;
  cursor: pointer;

  width: 20px;
  height: 20px;
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
