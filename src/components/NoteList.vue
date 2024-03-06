<template>
    <ul>
      <li v-for="(note, index) in notes" :key="index">
        {{ note.content }}
        <span>({{ note.content.split(' ').filter(Boolean).length }} mots)</span>
        <button @click="deleteNote(index)">Supprimer</button>
        <button @click="editNote(index)">Modifier</button> 
      </li>
    </ul>
  </template>
  
  <script>
  export default {
    props: ['notes'],
    methods: {
      deleteNote(index) {
        this.$emit('delete-note', index);
      },
      editNote(index) {
        this.$emit('edit-note', index); 
      }
    }
  }
  </script>
  
  <style>
 
  </style>
  