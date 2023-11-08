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
    <div class="navigation-menu">
      <img src="public/Cyber-Security-PNG-File.png" class="logo" alt="Logo" />
  
      <div class="menu-items">
        <router-link class="me-5" to="/">Home</router-link>
        <router-link class="me-5" to="/index">Index</router-link>
        <a href="http://127.0.0.1:8000/login">Login </a>
      </div>
    </div>

  </header>

  <main>
    <router-view></router-view>
  </main>

  <footer></footer>
</template>

<style lang="scss">


/* Stili specifici per il tuo menu di navigazione */
.navigation-menu {
  display: flex;
  align-items: center;
  //background: rgba(0, 0, 0, 0.3);
  padding:1rem;
  margin-left: 2rem;
  margin-right: 2rem;
}

.logo {
  width: 10rem; /* Larghezza del logo */
  margin-right: 20px; /* Spaziatura a destra del logo */
}

.menu-items {
  flex-grow: 1; /* Flessibilità per far crescere lo spazio disponibile */
  display: flex;
  justify-content: flex-end;
}

.menu-items a {
  color: #fff; /* Colore del testo delle voci del menu */
  text-decoration: none;
  margin-left: 20px; /* Spaziatura tra le voci del menu */
}
</style>
