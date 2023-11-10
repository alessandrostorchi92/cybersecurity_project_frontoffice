<script>
import axios from "axios";

export default {
  data() {
    return {
      profiles: [],
      specializations: [],
      minAverageScore: 0,
    };
  },

  watch: {
    minAverageScore: function () {
      this.fetchDataProfile();
    },
  },

  methods: {
    async fetchDataProfile() {
      console.log("Chiamato fetchDataProfile");

      await this.fetchSpecializationData();
      await this.fetchScoreFilterData();
    },

    async fetchSpecializationData() {
      const specializationName = this.$route.params.specialization;
      const apiUrlSpecialization = specializationName
        ? `http://127.0.0.1:8000/api/users/specialization/${specializationName}`
        : null;

      try {
        if (apiUrlSpecialization) {
          const response = await axios.get(apiUrlSpecialization);
          console.log("Risposta API Specializzazione:", response.data);
          // Gestisci la risposta come necessario
          // this.specializationData = response.data.data;
        }
      } catch (error) {
        console.error(
          "Errore durante il recupero dei dati di specializzazione:",
          error
        );
      }
    },

    async fetchScoreFilterData() {
      const apiUrlScoreFilter = `http://127.0.0.1:8000/api/profile/scoreFilter/${this.minAverageScore}`;

      try {
        const response = await axios.get(apiUrlScoreFilter);
        console.log("Risposta API Filtro Voti:", response.data);
        this.profiles = response.data.data;
      } catch (error) {
        console.error(
          "Errore durante il recupero dei dati del filtro dei voti:",
          error
        );
      }
    },

    getImageUrl(photo) {
      return `http://127.0.0.1:8000/storage/${photo}`;
    },
  },

  mounted() {
    this.fetchDataProfile();
  },
};
</script>

<template>
  <div class="container-fluid"></div>
  <div class="row">
    <div class="col-lg-4 col-12 categories-bg text-center">
      <header class="header">
        <strong><h1 class="title">Cyber Security</h1></strong>

        <p class="description ps-5 pe-5">
          Cyber Security è il punto di riferimento per esperti di sicurezza
          altamente qualificati. I nostri professionisti sono i guardiani
          digitali che proteggono il tuo mondo virtuale da minacce informatiche.
          Con competenze avanzate in analisi dei dati, crittografia e difesa
          cibernetica, ti offrono la tranquillità di navigare in modo sicuro nel
          vasto mare digitale. Scopri gli esperti di sicurezza di Cyber Sentinel
          e preparati a essere al sicuro online.
        </p>
        <router-link to="/" class="btn">Torna Indietro</router-link>
      </header>
      <label for="minAverageScore">Seleziona Media Voti:</label>
      <select v-model="minAverageScore" @change="fetchDataProfile">
        <option value="0">Mostra tutti</option>
        <option v-for="score in [1, 2, 3, 4, 5]" :key="score" :value="score">
          {{ score }}
        </option>
      </select>
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

      <div class="scrolling-container d-flex">
        <!-- Visualizza le card degli utenti -->
        <div class="row">
          <div class="col-md-4" v-for="user in profiles" :key="user.id">
            <div class="card mb-4">
              <img
                v-if="user.profile && user.profile.photo"
                :src="getImageUrl(user.profile.photo)"
                class="card-img-top"
                alt="Immagine Professionista"
              />
              <div class="card-body">
                <h5 class="card-title">{{ user.name }} {{ user.surname }}</h5>
                <div v-if="user.profile">
                  <p>Media: {{ user.average_score || "N/A" }}</p>
                  <div>
                    <p>Location: {{ user.profile.location }}</p>
                    <p>Skills: {{ user.profile.skills }}</p>
                    <p>Description: {{ user.profile.description }}</p>
                    <p>
                      Specialization:
                      {{
                        user.specializations
                          .map((specialization) => specialization.name)
                          .join(", ")
                      }}
                    </p>
                    <router-link :to="{ name: 'show', params: { id: user.id } }"
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
    </div>
  </div>

  <!-- ------------------------------ -->
</template>

<style lang="scss" scoped>
.title {
  font-size: 4rem;
  color: #27cdf2;
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
.bg-card {
  background-color: rgba(51, 51, 51, 0.9);
  color: #b0b1b2;
}
</style>
