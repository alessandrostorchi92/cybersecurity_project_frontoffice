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
	<div class="container-fluid">

		</div>
		<div class="row">
			<div class="col-lg-4 col-12 categories-bg text-center ">
								
				<header class="header">
					<h1 class="title ">Cyber Security</h1>
					<p class="description  p-3">
						La tua sicurezza informatica è di fondamentale importanza. Grazie alla nostra ricerca avanzata, puoi scoprire esperti specializzati nella tua zona, leggere le recensioni dei clienti e richiedere facilmente una consulenza. Con Cyber Security, avrai accesso a una rete di esperti affidabili pronti a proteggere il tuo mondo digitale. Non lasciare nulla al caso, affidati a noi per garantire la tua tranquillità online.
					</p>
					<router-link to="/index" class="btn ">Find Experts</router-link>
				</header>
				<!-- Contenuto delle categorie -->
				<div class="">
					<div class="text-center mt-5">
						<h5>Cerca la Categoria Desiderata</h5>
					</div>
					<div class="d-flex justify-content-center">
						<div class="badge-container text-center">
							<div class="next-arrow text-center"><i class="fa-solid fa-chevron-up"></i></div>
							<div v-for="(specialization, index) in specializations" :key="index"
								@click="selectSpecialization(specialization?.name)" @mouseover="showDescription(specialization)"
								@mouseout="selectedSpecialization = null" class="badge-style">
								{{ specialization?.name }}
							</div>
							<div class="prev-arrow text-center"><i class="fa-solid fa-chevron-down"></i></div>
						</div>
					</div>
				</div>
								<!-- descrizione catergorie  -->
								<div class="description-tooltip" v-if="selectedSpecialization">
									{{ selectedSpecialization.description }}
								</div>
								<!-- ------------------------------ -->
			</div>

			
			<div class="col-lg-8 col-12 ">

				<!-- bootstrap card -->

				<div class="scrolling-container  d-flex ">
					
						<!-- Contenuto della Card 1 -->
						<div class="card me-5" style="min-width: 18rem;">
							<img src="/profile-pic.webp" class="card-img-top" alt="...">
							<div class="card-body">
								<h5 class="card-text text-center">Nome Esperto</h5>
							</div>
						</div>
						<!------------------------->
						<div class="card me-5" style="min-width: 18rem;">
							<img src="/profile-pic.webp" class="card-img-top" alt="...">
							<div class="card-body">
								<h5 class="card-text text-center">Nome Esperto</h5>
							</div>
						</div>
						<div class="card me-5" style="min-width: 18rem;">
							<img src="/profile-pic.webp" class="card-img-top" alt="...">
							<div class="card-body">
								<h5 class="card-text text-center">Nome Esperto</h5>
							</div>
						</div>
						<div class="card me-5" style="min-width: 18rem;">
							<img src="/profile-pic.webp" class="card-img-top" alt="...">
							<div class="card-body">
								<h5 class="card-text text-center">Nome Esperto</h5>
							</div>
						</div>
						<div class="card me-5" style="min-width: 18rem;">
							<img src="/profile-pic.webp" class="card-img-top" alt="...">
							<div class="card-body">
								<h5 class="card-text text-center">Nome Esperto</h5>
							</div>
						</div>

					
				</div>

				<!-- -------------------------------- -->
			</div>
		</div>

	


</template>

<style lang="scss" scoped>
.title{
	font-size: 4rem;

}
.description{
	color: white;

}


.btn {
	cursor: pointer;
	background-color: rgb(37, 37, 37);
	color: #fff;
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
	margin-top: 32rem;
	margin-left: 2rem;
	
}




/*----------------------*/
.categories-bg {
	background-color: rgba(51, 51, 51, 0.9);
	color: #fff;
	height: 100vh;
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
	width: 15rem;
	text-align: center;
	margin: 5px;
	display: inline-block;
	padding: 8px 10px;
	background-color: rgb(37, 37, 37);
	color: white;

}

/* Stile per posizionare la descrizione delle categorie al centro */

.description-tooltip {
	background-color: rgb(37, 37, 37);
	border-radius: 15px;
	color: #fff;
	padding: 10px;
	text-align: center;
	max-width: 100%;
}

/*-----------------------------------------------*/





</style>
