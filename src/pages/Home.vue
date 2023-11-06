<script>
import SearchSpecialization from '../components/SearchSpecialization.vue';

export default {
	components: {
		SearchSpecialization
	},

	data() {
		return {

		};
	},
	methods: {

	},

	mounted() {

	},
};
</script>


<template>
	<div class="bg-image">
    <div class="">
        <div class="row justify-content-center">
            <div class=" col-md-7 col-sm-12 ">
                <h1 class="title">Cyber <br> Security</h1>
                <p class="description">La tua sicurezza informatica è importante. utilizza la nostra ricerca avanzata per scoprire esperti per specializazione e posizione,leggi le recensioni dei clienti e richiedi facilmente una consulenza. con Cyber Security , puoi accedere a una rete di esperti affidabili per proteggere il tuo mondo digitale.</p>
                <div class="d-flex justify-content-center">
                    <button  class="btn text-center">Cerca Esperti</button>
                </div>
            </div>
        </div>
    </div>
</div> 

	<div class="container">
		<h1>Homepage</h1>
		<SearchSpecialization></SearchSpecialization>
	</div>
</template>

<style lang="scss" scoped></style>