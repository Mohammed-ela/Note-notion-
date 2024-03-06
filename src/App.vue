<template>
  <div id="app">
    <NoteEditor @save-note="addOrUpdateNote" :existing-note="selectedNote" />
    <NoteList :notes="notes" @delete-note="deleteNote" @edit-note="editNote" />
  </div>
</template>

<script>
import NoteList from './components/NoteList.vue';
import NoteEditor from './components/NoteEditor.vue';

export default {
  name: 'App',
  components: {
    NoteEditor,
    NoteList
  },
  data() {
    return {
      notes: [],
      selectedNote: null, // Ajouté pour la gestion de la note sélectionnée pour modification
      selectedIndex: null // Conserver l'index de la note sélectionnée
    }
  },
  methods: {
    addOrUpdateNote(noteContent) {
      if (this.selectedNote && this.selectedIndex !== null) {
        // Mise à jour de la note existante
        this.notes[this.selectedIndex].content = noteContent;
        this.resetSelection();
      } else if (noteContent.trim() !== '') {
        // Ajout d'une nouvelle note
        this.notes.push({ content: noteContent });
      }
    },
    deleteNote(index) {
      this.notes.splice(index, 1);
    },
    editNote(index) {
      this.selectedNote = { ...this.notes[index] }; // Cloner la note pour éviter les modifications directes
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
/* Votre CSS ici */
</style>
