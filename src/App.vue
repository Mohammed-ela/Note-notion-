<template>
  <div id="app">
    <NoteEditor @save-note="addOrUpdateNote" :existing-note="selectedNote" />
    <NoteList :notes="notes" @delete-note="deleteNote" @edit-note="editNote" />
  </div>
</template>

<script>
import NoteEditor from './NoteEditor.vue'
import NoteList from './NoteList.vue'

export default {
  name: 'App',
  components: {
    NoteEditor,
    NoteList
  },
  data() {
    return {
      notes: [],
      selectedNote: null,
      selectedIndex: null
    }
  },
  created() {
    this.loadNotes();
  },
  methods: {
    loadNotes() {
      const notes = localStorage.getItem('notes');
      if (notes) {
        this.notes = JSON.parse(notes);
      }
    },
    saveNotes() {
      localStorage.setItem('notes', JSON.stringify(this.notes));
    },
    addOrUpdateNote(noteContent) {
      if (this.selectedNote && this.selectedIndex !== null) {
        this.notes[this.selectedIndex].content = noteContent;
        this.resetSelection();
      } else if (noteContent.trim() !== '') {
        this.notes.push({ content: noteContent });
      }
      this.saveNotes();
    },
    deleteNote(index) {
      this.notes.splice(index, 1);
      this.saveNotes();
    },
    editNote(index) {
      this.selectedNote = { ...this.notes[index] };
      this.selectedIndex = index;
    },
    resetSelection() {
      this.selectedNote = null;
      this.selectedIndex = null;
    }
  }
}
</script>

<style>

</style>
