<script>
import axios from "axios";
import StarRating from "../components/StarRating.vue";

export default {
  components: {
    StarRating,
  },

  props: {
    initialScore: {
      type: Number,
      default: 0,
    },
  },
  data() {
    return {
      profile: {},
      user: {},

      formData: {
        name: "",
        surname: "",
        email: "",
        description: "",
        user_id: ""
      },

      errors: null,
      success: null,
      reviewName: "",
      reviewSurname: "",
      reviewText: "",
      reviewScore: this.initialScore,
      reviewSubmitted: false,
      reviewError: false,
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

    submitReview() {
      const userId = this.$route.params.id;

      axios
        .post(`http://127.0.0.1:8000/api/reviews`, {
          user_id: userId,
          name: this.reviewName,
          surname: this.reviewSurname,
          text: this.reviewText,
          score: this.reviewScore,
        })
        .then((response) => {
          this.reviewSubmitted = true;
          this.reviewError = false;

          // Resetta i campi del form dopo l'invio
          this.reviewName = "";
          this.reviewSurname = "";
          this.reviewText = "";
          this.reviewScore = this.initialScore;
          this.reviewSubmitted = true;

          setTimeout(() => {
            this.reviewSubmitted = false;
            // this.$refs.starRating.resetStar();
          }, 1000);
        })

        .catch((error) => {
          console.error("Error submitting review:", error.response);
          this.reviewError = true;
          this.reviewSubmitted = false;
        });
    },

    getImageUrl(photo) {
      return `http://127.0.0.1:8000/storage/${photo}`;
    },

    onFormSubmit() {
      this.formData.user_id = this.profile.user_id;

      axios.post("http://localhost:8000/api/messages", this.formData)
        .then((response) => {
          this.success = response.data.message;
          this.errors = null;
        })
        .catch((error) => {
          this.errors = error.response?.data?.message ?? error.message;
        })
    },
    updateReviewScore(score) {
      this.reviewScore = score;
    },
  },

  mounted() {
    this.fetchData();
  },
};
</script>

<template>
  <div class="full-screen-card">
    <div class="card">
      <img v-if="profile.photo" :src="getImageUrl(profile.photo)" class="card-img-top" alt="Profile Image" />
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


  <!-- SEZIONE MESSAGGI -->
  <div class="container">
    <div class="row">
      <h1 class="pt-5">Contattami!</h1>

      <!-- messaggio errore -->
      <div class="alert alert-danger" v-if="errors">Sembra che tu non abbia compilato tutti i campi. Riprova!</div>

      <!-- form -->
      <form @submit.prevent="onFormSubmit" v-if="!success">

        <div class="mb-3">
          <label>Nome</label>
          <input type="text" class="form-control" v-model="formData.name">
        </div>

        <div class="mb-3">
          <label>Cognome</label>
          <input type="text" class="form-control" v-model="formData.surname">
        </div>

        <div class="mb-3">
          <label>Email</label>
          <input type="text" class="form-control" v-model="formData.email">
        </div>

        <div class="mb-3">
          <label>Messaggio</label>
          <textarea class="form-control" v-model="formData.description"></textarea>
        </div>

        <button type="submit" class="btn btn-primary mb-3">Invia</button>
      </form>

      <!-- messaggio invio SE a buon fine -->
      <div class="alert alert-success" v-else>{{ this.success }}</div>
    </div>

    <h1 class="pt-5">Scrivimi una recensione!</h1>

    <!-- Form recensione: -->
    <div class="card-body">
      <form @submit.prevent="submitReview">

        <div class="mb-3">
          <label for="score" class="form-label">Voto:</label>
          <star-rating :initial-score="reviewScore" @update-score="updateReviewScore" ref="starRating" />
        </div>
        <div class="mb-3">
          <label for="name" class="form-label">Nome:</label>
          <input type="text" v-model="reviewName" class="form-control" required />
        </div>

        <div class="mb-3">
          <label for="surname" class="form-label">Cognome:</label>
          <input type="text" v-model="reviewSurname" class="form-control" required />
        </div>

        <div class="mb-3">
          <label for="text" class="form-label">Recensione:</label>
          <textarea v-model="reviewText" class="form-control" required></textarea>
        </div>

        <button type="submit" class="btn btn-primary">Invia Recensione</button>
      </form>

      <!-- Messaggio di conferma o errore -->
      <div v-if="reviewSubmitted">
        <p class="mt-3 text-success">Recensione inviata con successo!</p>
      </div>
      <div v-if="reviewError">
        <p class="mt-3 text-danger">
          Si è verificato un errore durante l'invio della recensione.
        </p>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.full-screen-card {
  width: 100vw;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #f8f9fa;
  /* Cambia il colore dello sfondo a tuo piacimento */
}

.card {
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  background-color: #fff;
  width: 80vw;
  /* Imposta la larghezza della card (80% della larghezza della viewport) */
  max-width: 400px;
  /* Larghezza massima della card */
}

.card-img-top {
  object-fit: cover;
  width: 100%;
  height: 150px;
  /* Altezza dell'immagine */
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

/* Aggiunti stili per il componente StarRating */
.rating {
  font-size: 1.25rem;
  /* Imposta la dimensione del font delle stelle */
}

.stars-container {
  color: #ffc107;
  /* Colore delle stelle vuote */
}

.star {
  cursor: pointer;
}

.star.selected {
  color: #fdcc0d;
  /* Colore delle stelle piene */
}
</style>
