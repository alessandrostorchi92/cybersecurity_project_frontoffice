<script>
import Presentation from "./components/Presentation.vue";

export default {
  components: {
    Presentation,
  },

  data() {
    return {};
  },
  methods: {},

  mounted() {},
};
</script>

<template>
  <header>
    <div class="navigation-menu">
      <!-- colonna col-4 con bg-scuro -->
      <div class="row logo-column">
        <div class=" ">
          <img src="/logocyber.png" class="logo ms-3" alt="Logo" />
        </div>
      </div>

      <div class="menu-items">
        <router-link class="me-5" to="/">Home</router-link>
        <a class="me-3" href="http://127.0.0.1:8000/login">Login</a>
        <a class="me-3" href="http://127.0.0.1:8000/register">Register</a>
      </div>
    </div>
  </header>

  <main>
    <router-view></router-view>
  </main>

  <footer></footer>
</template>

<style lang="scss">
.navigation-menu {
  display: flex;
}

.logo-column {
  width: 33.73%;
  padding: 1rem;
}

.logo {
  width: 2.2rem;
}

.menu-items {
  flex-grow: 1;
  /* Flessibilità per far crescere lo spazio disponibile */
  display: flex;
  justify-content: flex-end;
  width: 60.63%;
  padding: 1rem;
  margin-right: 6rem;
}

.menu-items a {
  color: #b0b1b2;
  /* Colore del testo delle voci del menu */
  text-decoration: none;
}

.menu-items a:hover {
  border-bottom: 3px solid #27cdf2;
  color: black;
}
</style>
