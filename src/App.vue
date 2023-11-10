
<script>
import Presentation from './components/Presentation.vue';


export default {
  components: {
    Presentation,
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
  <Presentation></Presentation>

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
  width: 60.63%;
  padding: 1rem;
  margin-right: 6rem;
}

.menu-items a {
  color: #b0b1b2; /* Colore del testo delle voci del menu */
  text-decoration: none;
}
.menu-items a:hover{
  border-bottom: 3px solid #27CDF2 ;
  color: black;
}
</style>
