<script>
import axios from "axios";

export default {
  data() {
    return {
      profile: {},
      user: {},
    };
  },

  methods: {
    fetchData() {
      const userId = this.$route.params.id;

      axios
        .get(`http://127.0.0.1:8000/api/profile/${userId}`)
        .then((response) => {
          this.user = response.data.users.data[0];
          this.profile = response.data.profiles.data[0];
        })
        .catch((error) => {
          console.error("Error fetching data:", error);
        });
    },
    getImageUrl(photo) {
      return `http://127.0.0.1:8000/storage/${photo}`;
    },
  },

  mounted() {
    this.fetchData();
  },
};
</script>

<template>

  <div class="container-fluid">

  </div>
  <div class="row">
      <div class="col-lg-4 col-12 categories-bg text-center ">
                  
      <header class="header">
        
        <strong><h1 class="title">Cyber Security</h1></strong>
      
        <p class="description  ps-5 pe-5">
          Lorem, ipsum dolor sit amet consectetur adipisicing elit. Ducimus nostrum ipsam hic, delectus praesentium voluptates, sapiente quis ipsa, maxime obcaecati veniam provident optio sed magni id mollitia numquam natus consequatur.
        </p>
        <router-link to="/homepage" class="btn ">Torna Indietro</router-link> 
      </header>

      </div>

      
      <div class="col-lg-8 col-12 ">
          <div class="row">
              <div class="col-6"></div>
  
              <div class="col-5">
                  <header class="header text-center ">
                      <h2 class="reviews-title text-end">Professionista Eccezionale</h2>
                      <h4 class="reviews-font-color text-end mb-5">
                          E l'esperto di sicurezza eccezionale.Raccomandatissimo. 
                      </h4>
                      <div class="text-end">
                      <router-link to="/" class="btn">Contatta L'Esperto</router-link>
                  </div>
                  </header>
              </div>
          </div>
  

          <!-- bootstrap card -->

          <div class="scrolling-container  d-flex ">
                      <!-- Visualizza le card degli utenti -->
      <div class="row">
        <div class="card">
          <img
            :src="getImageUrl(profile.photo)"
            class="card-img-top"
            alt="Profile Image"
          />
          <div class="card-body">
            <h5 class="card-title">{{ user.name }} {{ user.surname }}</h5>
            <p class="card-text">Email: {{ user.email }}</p>
            <p v-if="user.specializations">
              Specializzazione:
              {{
                user.specializations
                  .map((specialization) => specialization.name)
                  .join(", ")
              }}
            </p>
            <p class="card-text">Phone: {{ profile.phone }}</p>
            <p class="card-text">Location: {{ profile.location }}</p>
            <p class="card-text">Descrizione: {{ profile.description }}</p>
          </div>
        </div>

      </div>
      

      
          
                  

              
          </div>

          <!-- -------------------------------- -->
      </div>
  </div>





  <!-- ----------------- -->
  
</template>

<style lang="scss" scoped>
.full-screen-card {
  width: 100vw;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #f8f9fa; /* Cambia il colore dello sfondo a tuo piacimento */
}

.card {
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  background-color: #fff;
  width: 80vw; /* Imposta la larghezza della card (80% della larghezza della viewport) */
  max-width: 400px; /* Larghezza massima della card */
}

.card-img-top {
  object-fit: cover;
  width: 100%;
  height: 150px; /* Altezza dell'immagine */
  border-top-left-radius: 10px;
  border-top-right-radius: 10px;
}

.card-body {
  padding: 20px;
}

.card-title {
  font-size: 1.5em;
  margin-bottom: 10px;
}

.card-text {
  margin-bottom: 8px;
}

.title{
	font-size: 4rem;
	color: #27CDF2;

}
.description{
	//color: white;
	color: #b0b1b2;
}
.reviews-title{
	color:#27CDF2;
	margin-bottom: 0;

}
.reviews-title h4{
	margin-top: -1.5rem;
}
.reviews-font-color{
	color: #b0b1b2;

}

.btn {
	cursor: pointer;
	background-color: rgb(37, 37, 37);
	color: #27CDF2;
	padding: 10px 20px;
	font-size: 1.2rem;
	text-decoration: none;
	border-radius: 5px;
	transition: background-color 0.3s;
	border-radius: 15px;
	text-align: center;
	padding: 8px 10px;
	width: 15rem;
}

.btn:hover {
	background-color: #6d7074;
}

/*----- Stile per il contenitore con uno scroll orizzontale -------*/
.scrolling-container {
	white-space: nowrap;
	/* Evita che le card si spezzino su più righe */
	overflow-x: auto;
	white-space: nowrap;
	margin-top: 5rem;
	margin-left: 2rem;
	
}
.bg-card{
	background-color:rgba(51, 51, 51, 0.9) ;
	color: #b0b1b2;;
}

</style>
