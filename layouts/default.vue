<template>
  <div>
    <nav-component></nav-component>
    <nuxt />
  </div>
</template>
<script>
import NavComponent from '~/components/NavComponent.vue'

export default {
  components:{
    NavComponent,
  },  
}
</script>

<style >
body{
  background-color: #FAFAFF;
}
</style>
