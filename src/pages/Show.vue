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
  <div class="full-screen-card">
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
</style>
