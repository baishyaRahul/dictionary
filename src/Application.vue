<template>
    <DictionaryApp />
  </template>
  
  <script>
  import DictionaryApp from './components/Dictionary.vue'
  
  export default {
    name: 'AppVTwo',
    components: {
        DictionaryApp
    }
  }
  </script>
  
  <style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
  </style>
  