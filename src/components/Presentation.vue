<script>
export default {
  data() {
    return {
      currentSlide: 1,
    };
  },
  methods: {
    nextSlide() {
      this.currentSlide += 1;
    },
    prevSlide() {
      this.currentSlide -= 1;
    },
  },
  
}
</script>
<template>
<div class="container-fluid">
  <div class="row ">
    <div class="col-lg-3 col-12 presentation-left  ">
      <img class="mt-5" src="public/cyber-security-boolean-logo.png" style="width: 23rem;" alt="">

        <div class="col-md-12 p-4 mar ">
          <p class="description flex-grow-1"><strong class="info">Maestro :</strong> Florian Leica</p>
          <p class="description"><strong class="info">Coordinatrore :</strong> Elisa Dahò</p>
          <p class="description"><strong class="info">Project Manager :</strong> Donato Riccio & Jacopo Damiani</p>
          <p class="description"><strong class="info">Studenti :</strong> alessandro Storchi, Amani Esseili, Dario Fusco, Ludovico Pellecchia e Stefano Priolo</p>


        </div>


    </div>


    <div class="col-lg-9 col-12 presentation-right ">
            <div class="row justify-content-center">
                <div class="col-md-10">
                  <div class="presentaion-bg">
                    <!-- ---------slide-1----------- -->
                    
                    <div v-if="currentSlide === 1" class="slide first-slide-bg col-md-6" id="slide-1">
                      
                      <h1 class="title slide1-title">Benvenuti nel Futuro della Sicurezza</h1>
                      <p class="description">Benvenuti alla presentazione della nostra app di sicurezza informatica. Siamo entusiasti di mostrarvi come abbiamo progettato un'app robusta e avanzata per proteggere i vostri dati sensibili, offrendo funzionalità di ricerca e analisi avanzate nel contesto della cyber security.</p>
                      <button class="btn" @click="nextSlide">Prossima Slide</button>

                    </div>
                    <!-- ---------slide-2----------- -->
                    <div v-else-if="currentSlide === 2" class="slide" id="slide-2">
                      <h2>Indice: Ricerca e Analisi</h2>
                      <p>Concept e progetto</p>
                      <button class="btn" @click="prevSlide">Indietro</button>
                      <button class="btn" @click="nextSlide">Prossima Slide</button>
                    </div>
                    <!-- ---------slide-3----------- -->
                    
                  </div>
                    



                </div>
            </div>
    </div>
</div>
</div>

<!-- ------------- -->



</template>
<style lang="scss" scoped>
/* stili per full body background */
.presentation-left {
	background-color:#202426;
	color: #fff;
	height: 100vh;
}
.presentation-right{
  background-image: url(/presentation-bg.jpg) ;
  background-attachment: fixed; //fissa il bg-img per evitare lo scrolling
	background-repeat: no-repeat; 
  background-size: contain;
  background-position: right;
  height: 100vh;
}

.mar{
  margin-top: 32rem;
}
.info{
  font-size: 1rem;
  color:  #1EBFCB;
  font-weight: bold

}

.title{
	font-size: 2rem;
	color:  #1EBFCB;

}
.description{
	color: #b0b1b2;
  font-size: 1rem;
}
.btn {
	cursor: pointer;
	background-color: rgb(37, 37, 37);
	color: #1EBFCB;
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

/*.first-slide-bg {
  margin: 0;
  //background-image: url('public/presentation-px2.jpg'); 
  background-attachment: fixed; //fissa il bg-img per evitare lo scrolling
	background-repeat: no-repeat; 
  background-size: cover;
  background-position: center;
  height: 100vh;
}*/

/* stili per il blocco della slide */
.slide {
  text-align: center;
  color: white;
  padding: 20px;
}

/* stili per gli stili specifici di ciascuna slide  */
/* stili specifici per la prima slide-1 */
#slide-1 {
  
  .slide1-title{
    margin-top: 20rem;
    //margin-right: 12rem;
  }
}
/*--------------------------------*/



</style>