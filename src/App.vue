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
<!-- colonna col-4 con bg-scuro -->
        <div class="row logo-column">
          <div class=" ">
            <img src="public/Cyber-Security-PNG-File.png" class="logo" alt="Logo" />
  
          </div>
        </div>
    
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



.navigation-menu {
  display: flex;
  //align-items: center;
  //background: rgba(0, 0, 0, 0.3);
  //padding:1rem;
  //margin-left: 2rem;
  //margin-right: 2rem;
  //height: 4rem;
}

.logo-column{
  background-color:rgba(51, 51, 51, 0.9) ;
  width: 33.73%;
  padding: 1rem;
}
.logo {
  width: 10rem; 
  margin-right: 20px; 
}

.menu-items {
  flex-grow: 1; /* Flessibilità per far crescere lo spazio disponibile */
  display: flex;
  justify-content: flex-end;
  width: 66.67%;
  padding: 1rem;
}

.menu-items a {
  color: #fff; /* Colore del testo delle voci del menu */
  text-decoration: none;
  margin-left: 20px; /* Spaziatura tra le voci del menu */
}
</style>
