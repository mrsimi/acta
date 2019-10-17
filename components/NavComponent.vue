<template>
<div>
  <a-menu
    id ="menu"
    mode="horizontal"
  >
    <a-menu-item key="mail">
      <nuxt-link to= "/" class="app-link"> Nigerian news aggregator website</nuxt-link>
    </a-menu-item>
  </a-menu>

  <!-- <nav>
      <h2> Nigerian news aggregator website</h2>
  </nav> -->
</div>
</template>

<script>

</script>

<style scoped>

#menu{
    text-align: center;
    text-transform: uppercase;
}

/* nav{
    text-align: center;
    padding: 20px 5px;
    border-bottom: 1px solid #ddd;
} */
</style>