<script>
import axios from "axios";

export default {
  data() {
    return {
      specializations: [],
      selectedSpecialization: null,
      premiumUsers: [], // Array per i dati degli utenti "premium"
    };
  },
  methods: {
    getSpecializationsFromApi() {
      axios.get("http://127.0.0.1:8000/api/specialization").then((response) => {
        this.specializations = response.data;
      });
    },

    selectSpecialization(specializationId) {
      this.$router.push({
        name: "index",
        params: { specialization: specializationId },
      });
    },

    showDescription(specialization) {
      this.selectedSpecialization = specialization;
    },

    getPremiumUsersFromApi() {
      axios.get("http://127.0.0.1:8000/api/premium-users").then((response) => {
        this.premiumUsers = response.data;
      });
    },

    getImageUrl(photo) {
      return `http://127.0.0.1:8000/storage/${photo}`;
    },
  },

  mounted() {
    this.getSpecializationsFromApi();
    this.getPremiumUsersFromApi();
  },
};
</script>

<template>
  <div class="row">
    <div class="col-lg-4 col-12 categories-bg text-center">
      <header class="header">
        <strong>
          <h1 class="title">Cyber Security</h1>
        </strong>

        <p class="description ps-5 pe-5">
          La tua sicurezza informatica è fondamentale. Scopri esperti
          specializzati, leggi recensioni e richiedi consulenza con Cyber
          Security. Proteggi il tuo mondo digitale con noi.
        </p>
        <!-- <router-link to="/index" class="btn ">Find Experts</router-link> -->
      </header>
      <!-- Contenuto delle categorie -->
      <div class="">
        <div class="text-center mt-5">
          <h5 class="title-cat-color">Cerca la Categoria Desiderata</h5>
        </div>
        <div class="d-flex justify-content-center">
          <div class="badge-container text-center">
            <div class="next-arrow text-center">
              <i class="fa-solid fa-chevron-up"></i>
            </div>
            <div
              v-for="(specialization, index) in specializations"
              :key="index"
              @click="selectSpecialization(specialization?.id)"
              @mouseover="showDescription(specialization)"
              @mouseout="selectedSpecialization = null"
              class="badge-style btn btn-primary"
            >
              {{ specialization?.name }}
            </div>
            <div class="prev-arrow text-center">
              <i class="fa-solid fa-chevron-down"></i>
            </div>
          </div>
        </div>
      </div>
      <!-- descrizione catergorie  -->
      <div class="description-tooltip" v-if="selectedSpecialization">
        {{ selectedSpecialization.description }}
      </div>
      <!-- ------------------------------ -->
    </div>

    <div class="col-lg-8 col-12">
      <div class="row">
        <div class="col-6"></div>

        <div class="col-5">
          <header class="header text-center">
            <h2 class="slogan text-end">Sicurezza Digitale su Misura</h2>
            <h4 class="slogan-font-color text-end mb-5">
              La Tua Difesa Online
            </h4>
          </header>
        </div>
      </div>

      <!-- Stampa le card degli utenti che hanno una sponsorizzazione attiva -->
      <div class="container">
        <div class="row">
          <div class="col-md-4" v-for="user in premiumUsers" :key="user.id">
            <div class="card my-3 bg-card ms-4" style="width: 18rem">
              <div class="card-body">
                <img
                  :src="getImageUrl(user.profile.photo)"
                  class="card-img-top mb-2"
                  alt="Immagine dell'utente"
                />
                <h5 class="card-title py-2">
                  {{ user.name }} {{ user.surname }}
                  <i class="fa-solid fa-crown text-warning"></i>
                </h5>
                <h6 class="card-subtitle mb-2 text-info">Specializzazioni:</h6>
                <ul>
                  <li
                    v-for="specialization in user.specializations"
                    :key="specialization.id"
                  >
                    {{ specialization.name }}
                  </li>
                </ul>
                <p class="card-text">{{ user.profile.description }}</p>
                <router-link
                  class="btn btn-primary"
                  :to="{ name: 'show', params: { id: user.id } }"
                  >Dettagli</router-link
                >
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- -------------------------------- -->
</template>

<style lang="scss" scoped>
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

.title {
  font-size: 4rem;
  color: #27cdf2;
}

.description {
  //color: white;
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
  margin-top: 22rem;
  margin-left: 2rem;
}

.bg-card {
  background-color: rgba(51, 51, 51, 0.6);
  color: #b0b1b2;
}

/*----------------------*/
.categories-bg {
  border-top-right-radius: 40px;
  background-color: rgba(51, 51, 51, 0.6);
  color: #fff;
}

.title-cat-color {
  color: #b0b1b2;
}

.badge-container {
  align-self: center;

  scrollbar-width: none;
  /* Nasconde le barre di scorrimento standard Firefox */
  -ms-overflow-style: none;
  /* Nasconde le barre di scorrimento standard IE/Edge */

  &::-webkit-scrollbar {
    width: 0;
  }
}

.badge-style {
  cursor: pointer;
  border-radius: 15px;
  width: 15rem;
  text-align: center;
  margin: 5px;
  display: inline-block;
  padding: 8px 10px;
  background-color: rgb(37, 37, 37);
  color: #b0b1b2;
}

/* Stile per posizionare la descrizione delle categorie al centro */

.description-tooltip {
  background-color: rgb(37, 37, 37);
  border-radius: 15px;
  color: #b0b1b2;
  padding: 10px;
  text-align: center;
  max-width: 100%;
}

/*-----------------------------------------------*/
</style>
