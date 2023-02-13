<template>
    <formRegister/>
  </template>
  
  <script>
  import { defineComponent } from 'vue';
  
  // Components
  import formRegister from '../components/formRegister.vue';
  
  export default defineComponent({
    name: 'RegisterView',
  
    components: {
      formRegister,
    },
  });
  </script>
  