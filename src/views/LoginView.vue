<template>
  <formLogin/>
</template>

<script>
import { defineComponent } from 'vue';

// Components
import formLogin from '../components/formLogin.vue';

export default defineComponent({
  name: 'LoginView',

  components: {
    formLogin,
  },
});
</script>
