<script>

export default {
  components: {
  },

  data() {
    return {

    };
  },
  methods: {

  },

  mounted() {

  },

};

</script>


<template>
  <header>
    <nav class="navbar navbar-expand-md navbar-light bg-white shadow-sm">
      <div class="container">
        <a class="navbar-brand d-flex align-items-center" href="#">
          <div>LOGO</div>
        </a>
        <ul class="navbar-nav me-auto">
          <li class="nav-item"><router-link class="nav-link" to="/">Home</router-link></li>
          <li class="nav-item"><router-link class="nav-link" to="/index">Index</router-link></li>
          <li class="nav-item"><router-link class="nav-link" to="/show">Show</router-link></li>
        </ul>
      </div>
    </nav>
  </header>

  <main>
    <router-view></router-view>
  </main>

  <footer></footer>
</template>

<style lang="scss"></style>
