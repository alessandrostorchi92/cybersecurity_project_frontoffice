<script>
import axios from "axios";

export default {
    data() {
        return {
            specializations: [],
        };
    },
    methods: {
        getSpecializationsFromApi() {
            axios.get("http://127.0.0.1:8000/api/specialization").then((response) => {
                this.specializations = response.data;
            });
        },

        selectSpecialization(specializationName) {
            this.$router.push({ name: 'index', params: { specialization: specializationName } });
        },
    },

    mounted() {
        this.getSpecializationsFromApi();
    },
};
</script>

<template>
    <div class="bg-image">
        <div class="container">
            <div class="row justify-content-center">
                <div class=" col-md-7 col-sm-12 ">
                    <h1 class="title">Cyber <br> Security</h1>
                    <p class="description">La tua sicurezza informatica è importante. utilizza la nostra ricerca avanzata
                        per scoprire esperti per specializazione e posizione,leggi le recensioni dei clienti e richiedi
                        facilmente una consulenza. con Cyber Security , puoi accedere a una rete di esperti affidabili per
                        proteggere il tuo mondo digitale.</p>
                    <div class="d-flex justify-content-center">
                        <router-link class="btn text-center" to="/index">Cerca Esperti</router-link>
                    </div>
                </div>
            </div>
            <div class="badge-container text-end">
                <div v-for="(specialization, index) in specializations" :key="index" class="badge-style"
                    @click="selectSpecialization(specialization.name)">
                    {{ specialization.name }}
                </div>
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
}
</style>