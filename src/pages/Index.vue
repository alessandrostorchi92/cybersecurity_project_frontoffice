<script>
import axios from "axios";

export default {
  data() {
    return {
      profiles: [],
      average_score: 0,
      specializations: [],
      minAverageScore: 0,
      specializationId: 0,
      minReviewCount: 0,
    };
  },
  methods: {
    async fetchDataProfile() {
      this.profiles = await this.fetchUsersBySpecialization();
    },

    async fetchUsersBySpecialization() {
      const apiUrlSpecialization = this.specializationId
        ? `http://127.0.0.1:8000/api/users/specialization/${this.specializationId}`
        : null;

      try {
        if (apiUrlSpecialization) {
          const response = await axios.get(apiUrlSpecialization);
          return response.data.data;
        }
      } catch (error) {
        console.error(
          "Errore durante il recupero dei dati di specializzazione:",
          error
        );
      }
    },

    getImageUrl(photo) {
      return `http://127.0.0.1:8000/storage/${photo}`;
    },

    displayStars(averageScore) {
      const roundedScore = Math.round(averageScore);
      const starCount = 5;

      // Creiamo una stringa di stelle basata sulla media dei voti utilizzando le icone di Font Awesome
      const fullStar = '<i class="fas fa-star" style="color: #fdcc0d;"></i>';
      const emptyStar = '<i class="far fa-star" style="color: #fdcc0d;"></i>';
      const stars =
        fullStar.repeat(roundedScore) +
        emptyStar.repeat(starCount - roundedScore);

      return `<span class="fa-stack fa-lg">${stars}</span>`;
    },
  },

  mounted() {
    this.specializationId = this.$route.params.specialization;
    this.fetchDataProfile();
  },
};
</script>

<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col-12 col-lg-4 categories-bg text-center">
        <header class="header">
          <strong><h1 class="title">Cyber Security</h1></strong>

          <p class="description ps-5 pe-5">
            Cyber Security è il punto di riferimento per esperti di sicurezza
            altamente qualificati. I nostri professionisti sono i guardiani
            digitali che proteggono il tuo mondo virtuale da minacce
            informatiche. Con competenze avanzate in analisi dei dati,
            crittografia e difesa cibernetica, ti offrono la tranquillità di
            navigare in modo sicuro nel vasto mare digitale. Scopri gli esperti
            di sicurezza di Cyber Sentinel e preparati a essere al sicuro
            online.
          </p>
          <router-link to="/" class="btn">Torna Indietro</router-link>
        </header>
        <div class="row flex-column justify-content-center p-5">
          <div class="col-4 pb-3">
            <label for="minAverageScore" class="form-label"
              >Seleziona Media Voti:</label
            >
            <select
              v-model="minAverageScore"
              @change="fetchDataProfile"
              class="form-select"
            >
              <option value="0">Mostra tutti</option>
              <option
                v-for="score in [1, 2, 3, 4, 5]"
                :key="score"
                :value="score"
              >
                {{ score }}
              </option>
            </select>
          </div>
          <div class="col-4">
            <label for="numeroRecensioni" class="form-label"
              >Seleziona utenti con più di:</label
            >
            <select
              v-model="minReviewCount"
              @change="fetchDataProfile"
              class="form-select"
            >
              <option value="0">Mostra tutti</option>
              <option v-for="count in [1, 5, 10]" :key="count" :value="count">
                {{ count }} recensioni
              </option>
            </select>
          </div>
        </div>
      </div>

      <div class="col-lg-8 col-12">
        <div class="row">
          <div class="col-6"></div>

          <div class="col-5">
            <header class="header text-center">
              <h2 class="slogan text-end">Esperti di Sicurezza</h2>
              <h4 class="slogan-font-color text-end mb-5">
                Il Tuo Scudo Digitale nel Mondo Virtuale
              </h4>
              <div class="text-end">
                <router-link to="/" class="btn"
                  >Controlla Disponibilita</router-link
                >
              </div>
            </header>
          </div>
        </div>

        <!-- bootstrap card -->

        <!-- Visualizza le card degli utenti -->
        <div class="row scrolling-container">
          <div class="col-md-4" v-for="user in profiles" :key="user.id">
            <div
              class="card scroll-card bg-card mb-4"
              v-if="
                !isNaN(user.average_score) &&
                user.average_score >= minAverageScore &&
                !isNaN(user.review_count) &&
                user.review_count >= minReviewCount
              "
            > 
              <img
                v-if="user.profile && user.profile.photo"
                :src="getImageUrl(user.profile.photo)"
                class="card-img-top"
                alt="Immagine Professionista"
              />
              <div class="card-body overflow-auto  flex-column p-1">
                <h5 class="card-title mb-2">{{ user.name }} {{ user.surname }}</h5>
                <div class="details " v-if="user.profile">
                  <p class="mb-2">
                    Valutazione:
                    <span v-html="displayStars(user.average_score)"></span>
                  </p>
                  <p class="mb-2">
                    Numero di recensioni:
                    <span class="review-count">{{
                      user.review_count || 0
                    }}</span>
                  </p>
                  <div class="card-text mb-3">
                    <p>Location: {{ user.profile.location }}</p>
                    <p>Skills: {{ user.profile.skills }}</p>
                    <p style="word-wrap: break-word">Description: {{ user.profile.description }}</p>
                    <p>
                      Specialization:
                      {{
                        user.specializations
                          .map((specialization) => specialization.name)
                          .join(", ")
                      }}
                    </p>
                    <router-link class="link" :to="{ name: 'show', params: { id: user.id } }"
                      >Dettagli</router-link
                    >
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- -------------------------------- -->
      </div>
    </div>
  </div>
  <!-- ------------------------------ -->
</template>

<style lang="scss" scoped>



body{
	background-image: url(/bg-2.jpg);
	background-size: cover;
	background-attachment: fixed; //fissa il bg-img per evitare lo scrolling
	background-repeat: no-repeat;

}
/* aggiunge un overlay trasparente all'immagine di sfondo */
body::before {
  content: "";
  background: rgba(173, 171, 171, 0.5); 
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: -1; /* Posiziona l'overlay dietro all'immagine di sfondo */
}

.categories-bg {
	background-color: rgba(51, 51, 51, 0.9);
	color: #fff;
	height: 100vh;
}


/* ----------------------------------------- */
.title{
	font-size: 4rem;
	color: #27CDF2;

}
.description {
  //color: white;
  color: #b0b1b2;
}
.slogan {
  color: #27cdf2;
  margin-bottom: 0;
}
.slogan h4 {
  margin-top: -1.5rem;
}
.slogan-font-color {
  color: #b0b1b2;
}

.btn {
  cursor: pointer;
  background-color: rgb(37, 37, 37);
  color: #27cdf2;
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

.scroll-card {
  height: 350px; /* Imposta l'altezza fissa del contenitore */
}

.bg-card {
  background-color: rgba(51, 51, 51, 0.5);
  color: #b0b1b2;
}
.card-body {
  
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}
.link{
  color: #27CDF2;
}
</style>
