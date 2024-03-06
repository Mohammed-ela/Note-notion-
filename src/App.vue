<template>
  <div>
    <NoteList :notes="notes" @delete-note="deleteNote" @edit-note="editNote"/>
    <NoteEditor @save-note="saveNote"/>
  </div>
</template>

<script>
import NoteList from './components/NoteList.vue';
import NoteEditor from './components/NoteEditor.vue';

export default {
  components: {
    NoteList,
    NoteEditor
  },
  data() {
    return {
      notes: JSON.parse(localStorage.getItem('notes')) || []
    };
  },
  methods: {
    saveNote(note) {
      this.notes.push(note);
      this.updateLocalStorage();
    },
    deleteNote(noteIndex) {
      this.notes.splice(noteIndex, 1);
      this.updateLocalStorage();
    },
    editNote(noteIndex, newNote) {
      this.notes[noteIndex] = newNote;
      this.updateLocalStorage();
    },
    updateLocalStorage() {
      localStorage.setItem('notes', JSON.stringify(this.notes));
    }
  }
}
</script>
