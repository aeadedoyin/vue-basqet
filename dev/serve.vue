<script>
import Vue from 'vue';
import VueBasqet from '@/vue2-basqet.vue';

export default Vue.extend({
  name: 'ServeDev',
  components: {
    VueBasqet
  }
});
</script>

<template>
  <div id="app">
    <vue2-basqet>Pay</vue2-basqet>
  </div>
</template>
