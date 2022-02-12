<script>
import Vue from 'vue';
import VueBasqet from '@/vue-basqet.vue';

export default Vue.extend({
  name: 'ServeDev',
  components: {
    VueBasqet
  }
});
</script>

<template>
  <div id="app">
    <vue-basqet>Pay</vue-basqet>
  </div>
</template>
