<script>
import axios from 'axios';

export default {
    components: {},
    data() {
        return {
            specializations: [],
            selectedIndex: 0, // Inizializza l'indice selezionato a 0
        };
    },
    methods: {
        getSpecializationsFromApi() {
            axios.get("http://127.0.0.1:8000/api/specialization")
                .then((response) => {
                    this.specializations = response.data;
                });
        },
        getBadgeSize(index) {
            return {
                'large-badge': this.selectedIndex === index,
/*                 'medium-lg-badge': Math.abs(this.selectedIndex - index) === 1,
                'medium-md-badge': Math.abs(this.selectedIndex - index) === 2,
                'medium-sm-badge': Math.abs(this.selectedIndex - index) === 3,
                'small-badge': this.selectedIndex !== index */
            }
        },
        clickSize(index) {
            this.selectedIndex = index; // Imposta l'indice selezionato
        },
        nextBadgeSlide() {
            this.selectedIndex = (this.selectedIndex + 1) % this.specializations.length; // Scorrimento all'elemento successivo o al primo
        },
        prevBadgeSlide() {
            this.selectedIndex = (this.selectedIndex - 1 + this.specializations.length) % this.specializations.length; // Scorrimento all'elemento precedente o all'ultimo
        },
    },
    computed: {
        centerIndex() {
            return Math.floor(this.specializations.length / 2);
        },
    },
    mounted() {
        this.getSpecializationsFromApi()
    },
};
</script>



<template>
    <div class="container">
        <div class="text-center mt-5">
            <h2>Trova l'esperto che fa al caso tuo!</h2>
            <h4>Seleziona una categoria e comincia la tua ricerca</h4>
        </div>

        <div class="d-flex justify-content-between mt-5">

            <div class="description-container"></div>
            <div class="badge-container text-end">
                <div class="next-arrow text-center" @click="nextBadgeSlide()"><i class="fa-solid fa-chevron-up"></i></div>

                <div v-for="(specialization, index) in specializations">
                    <div class="badge-style" :class="getBadgeSize(index)" @click="clickSize(index)">{{ specialization?.name
                    }}</div>
                </div>
                <div class="prev-arrow text-center" @click="prevBadgeSlide()"><i class="fa-solid fa-chevron-down"></i></div>

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

.large-badge {
    transform: scale(1) !important;
}

.medium-lg-badge {
    transform: scale(0.90) !important;
}

.medium-md-badge {
    transform: scale(0.83) !important;
}

.medium-sm-badge {
    transform: scale(0.73) !important;
}

.small-badge {
    transform: scale(0.65);
}
</style>