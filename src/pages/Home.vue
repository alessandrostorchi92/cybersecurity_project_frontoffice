<script>
import axios from "axios";

export default {
    data() {
        return {
            specializations: [],
            selectedSpecialization: null
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

        showDescription(specialization) {
            this.selectedSpecialization = specialization;
        },
    },

    mounted() {
        this.getSpecializationsFromApi();
    },
};
</script>

<template>
    <div class="home-container">
        <header class="header">
            <h1 class="title">Cyber Security</h1>
            <p class="description">
                Your online security is important. Use our advanced search to find experts by specialization and location,
                read customer reviews, and easily request a consultation. With Cyber Security, you can access a network of
                trusted experts to protect your digital world.
            </p>
            <router-link to="/index" class="btn">Find Experts</router-link>
        </header>

        <div class="specializations">
            <div v-for="(specialization, index) in specializations" :key="index"
                @click="selectSpecialization(specialization.name)" @mouseover="showDescription(specialization)"
                @mouseout="selectedSpecialization = null" class="specialization-badge">
                {{ specialization.name }}
            </div>
            <div class="description-tooltip" v-if="selectedSpecialization">
                {{ selectedSpecialization.description }}
            </div>
        </div>
    </div>
</template>

<style lang="scss" scoped>
.home-container {
    background: linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)), url('your-background-image.jpg');
    background-size: cover;
    background-position: center;
    color: #fff;
    text-align: center;
    padding: 100px 0;
}

.header {
    max-width: 800px;
    margin: 0 auto;
}

.title {
    font-size: 2.5rem;
    margin-bottom: 20px;
}

.description {
    font-size: 1.2rem;
    margin-bottom: 40px;
}

.btn {
    background-color: #007bff;
    color: #fff;
    padding: 10px 20px;
    font-size: 1.2rem;
    text-decoration: none;
    border-radius: 5px;
    transition: background-color 0.3s;
}

.btn:hover {
    background-color: #0056b3;
}

.specializations {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    margin-top: 40px;
}

.specialization-badge {
    cursor: pointer;
    background-color: #333;
    color: #fff;
    border-radius: 10px;
    /* Badge più piccoli */
    padding: 8px 16px;
    /* Dimensioni ridotte */
    margin: 0 10px 10px;
    font-size: 1rem;
    /* Testo più piccolo */
    position: relative;
    transition: background-color 0.3s;
}

@media screen and (max-width: 768px) {
    .header {
        padding: 20px;
    }

    .title {
        font-size: 2rem;
    }

    .description {
        font-size: 1rem;
    }

    .btn {
        font-size: 1rem;
    }

    .specialization-badge {
        font-size: 1rem;
        padding: 6px 12px;
    }
}
</style>
