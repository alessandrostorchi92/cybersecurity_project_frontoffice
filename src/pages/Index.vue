<script>
import axios from 'axios';

export default {


    data() {
        return {
            users:[],
            specializations: [],
            selectedSpecialization: null, // Aggiungi una variabile per memorizzare la specializzazione selezionata
        };
    },
    methods: {
        fetchData() {
            axios
                .get('http://127.0.0.1:8000/api/users', {
                    params: {
                        specialization: this.selectedSpecialization // Passa il nome della specializzazione come parametro
                    }
                })
                .then((response) => {
                    this.users = response.data.data;
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

            this.fetchData();
        },

    },

    mounted() {
        this.getSpecializationsFromApi()

    },
};
</script>


<template>
    <div class="container">
        <h1>Index</h1>
    </div>
<ul v-for="user in users">
    <li><router-link :to="{name:'show', params: {id: user.id}}">{{ user.name}}</router-link></li>
</ul>
<div class="container">
        <div class="text-center mt-5">
            <h2>Trova l'esperto che fa al caso tuo!</h2>
            <h4>Seleziona una categoria e comincia la tua ricerca</h4>
        </div>

        <div class="d-flex justify-content-between mt-5">

            <div class="description-container"></div>
            <div class="badge-container text-end">
                <div class="next-arrow text-center"><i class="fa-solid fa-chevron-up"></i></div>
                <div v-for="(specialization, index) in specializations" :key="index">
                    <div class="badge-style" @click="selectSpecialization(specialization?.name), fetchData()">
                        {{ specialization?.name }}
                    </div>
                </div>
                <div class="prev-arrow text-center"><i class="fa-solid fa-chevron-down"></i></div>
            </div>
        </div>
    </div>
</template>

<style lang="scss" scoped>
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

}</style>