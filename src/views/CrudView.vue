<template>
    <crud/>
  </template>
  
  <script>
  import { defineComponent } from 'vue';
  
  // Components
  import crud from '../components/crud.vue';
  
  export default defineComponent({
    name: 'ProductRegisterView',
  
    components: {
      crud,
    },
  });
  </script>
  