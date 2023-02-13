<template>
  <carrousel />
</template>

<script>
import { defineComponent } from 'vue';

// Components
import carrousel from '../components/carrousel.vue';

export default defineComponent({
  name: 'HomeView',

  components: {
    carrousel,
  },
});
</script>
