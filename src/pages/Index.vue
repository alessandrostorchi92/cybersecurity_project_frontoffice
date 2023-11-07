<script>
import axios from "axios";

export default {

    data() {
        return {
            profiles: [],
            specializations: [],
            selectedSpecialization: null, // Aggiungi una variabile per memorizzare la specializzazione selezionata
        };
    },
    methods: {

        fetchDataProfile() {
            axios.get(`http://127.0.0.1:8000/api/users/specialization/${this.selectedSpecialization}`)
                .then((response) => {
                    this.profiles = response.data.data;
                });
        },

        getSpecializationsFromApi() {
            axios.get("http://127.0.0.1:8000/api/specialization")
                .then((response) => {
                    this.specializations = response.data;
                });
        },

        selectSpecialization(specializationName) {
            this.selectedSpecialization = specializationName; // Memorizza il nome della specializzazione selezionata

            this.fetchDataProfile()
        },

        getImageUrl(photo) {
            return `http://127.0.0.1:8000/storage/${photo}`;
        },
    },

    mounted() {
        this.fetchDataProfile();
        this.getSpecializationsFromApi();
    },
};
</script>

<template>
    <div class="container">
        <h1>Index</h1>
        <!-- Visualizza le card degli utenti -->
        <div class="row gap-5 my-row">
            <div class="col-md-4" v-for="user in profiles" :key="user.id">
                <div class="card mb-4">
                    <img :src="getImageUrl(user.profile.photo)" class="card-img-top" alt="Immagine Professionista" />
                    <div class="card-body">
                        <h5 class="card-title">{{ user.name }} {{ user.surname }}</h5>
                        <div v-if="user.profile">
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
                                <router-link :to="{ name: 'show', params: { id: user.id } }">Dettagli</router-link>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <div class="col-md-3 my-col">
                <div class="text-center mt-5">
            <h4>Seleziona una categoria e comincia la tua ricerca</h4>
        </div>
            <div class="d-flex justify-content-center mt-5">
                <div class="badge-container text-end">
                    <div class="next-arrow text-center"><i class="fa-solid fa-chevron-up"></i></div>
                    <div v-for="(specialization, index) in specializations" :key="index">
                        <div class="badge-style" @click="selectSpecialization(specialization?.name)">
                            {{ specialization?.name }}
                        </div>
                    </div>
                    <div class="prev-arrow text-center"><i class="fa-solid fa-chevron-down"></i></div>
                </div>
            </div>
        </div>



        </div>

    </div>
</template>
  

<style lang="scss" scoped>

.my-row{
    position: relative;

    .my-col{
        position: absolute;
        right: 0;
    }
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
    width: 240px;
    text-align: center;
    margin: 5px;
    display: inline-block;
    padding: 8px 10px;
    background-color: rgb(37, 37, 37);
    color: white;

}
</style>