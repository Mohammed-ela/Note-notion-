<template>
    <div>
      <textarea v-model="noteContent" placeholder="Écrivez quelque chose ici..."></textarea>
      <button @click="handleSave">{{ isEditing ? 'Modifier' : 'Sauvegarder' }}</button>
    </div>
  </template>
  
  <script>
  export default {
    props: ['existingNote'],
    data() {
      return {
        noteContent: ''
      }
    },
    watch: {
      existingNote: {
        immediate: true,
        handler(newValue) {
          this.noteContent = newValue ? newValue.content : '';
        }
      }
    },
    computed: {
      isEditing() {
        return !!this.existingNote;
      }
    },
    methods: {
      handleSave() {
        if (this.noteContent.trim()) {
          this.$emit('save-note', this.noteContent);
          this.noteContent = ''; // Réinitialiser seulement si c'est une nouvelle note
        } else {
          alert("Veuillez écrire quelque chose avant de sauvegarder.");
        }
      }
    }
  }
  </script>
  
  <style>

  </style>
  