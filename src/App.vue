<script setup>

</script>

<template>
  <!-- NAVBAR -->
  <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
    <div class="container-fluid">
      <router-link class="navbar-brand" to="/">
        <img
          src="https://cdn-icons-png.flaticon.com/512/188/188987.png" alt="Logo"
          width="30" height="24"
          class="d-inline-block align-text-top"
      >
        PokeVite
      </router-link>
    </div>
  </nav>

  <!-- CONTENT -->
  <div class="main">
    <router-view></router-view>
  </div>

  <footer class="bg-dark text-light">
    <div>Design in {{ new Date().getFullYear() }}</div>
  </footer>

</template>

<style>
  body{
    overflow: hidden;
    min-height: 100vh;
    background: #fff;
  }
  footer{
    position: fixed;
    bottom: 0;
    width: 100%;
    display: flex;
    align-items:center;
    justify-content: center;
    height: 56px;
  }
  @media (max-width: 600px) {
    body{
      overflow: auto;
    }
  }
</style>