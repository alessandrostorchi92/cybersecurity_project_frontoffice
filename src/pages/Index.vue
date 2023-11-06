<script>
import axios from "axios";
import SearchSpecialization from "../components/SearchSpecialization.vue";

export default {
    components: {
        SearchSpecialization,
    },
    data() {
        return {
            profiles: [],
            filteredProfiles:[]
        };
    },
    methods: {
        fetchDataProfile() {
            axios
                .get("http://127.0.0.1:8000/api/profile")
                .then((response) => {
                    console.log(response.data);
                    this.profiles = response.data.data;
                })
                .catch((error) => {
                    console.error("Error fetching profile data:", error);
                });
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
    <div class="container">
        <h1>Index</h1>
        <!-- Visualizza le card degli utenti -->
        <div class="row gap-5">
            <div class="col-8">
                <div class="col-2" v-for="user in profiles" :key="user.id" style="width: 18rem">
                    <div class="card">
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
            </div>

            <div class="col-3">
                <SearchSpecialization></SearchSpecialization>
            </div>

        </div>
    </div>
</template>

<style lang="scss" scoped></style>