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
          <p class="description"><strong class="info">Studenti :</strong> alessandro Storchi, Amani Esseili, Dario Fusco,
            Ludovico Pellecchia e Stefano Priolo</p>
        </div>
      </div>


      <div class="col-lg-9 col-12 presentation-right ">
        <div class="row justify-content-center">
          <div class="col-md-10">
            <div class="presentaion-bg">
              <!-- ---------slide-1----------- -->

              <div v-if="currentSlide === 1" class="slide first-slide-bg col-md-6" id="slide-1">

                <h1 class="title slide1-title">Benvenuti nel Futuro della Sicurezza</h1>
                <p class="description">Benvenuti alla presentazione della nostra app di sicurezza informatica. Siamo
                  entusiasti di mostrarvi come abbiamo progettato un'app robusta e avanzata per proteggere i vostri dati
                  sensibili, offrendo funzionalità di ricerca e analisi avanzate nel contesto della cyber security.</p>
                <button class="btn" @click="nextSlide">Prossima Slide</button>

              </div>
              <!-- ---------slide-2----------- -->
              <div v-else-if="currentSlide === 2" class="slide col-10" id="slide-2">

                <h2 class="title">Che cos'è CyberSecurity ? </h2>
                <p class="description">CyberSecure e un app che fa la differenza nell’era digitale. La crescente minnaccia
                  delle violazioni delle sicurezza digitale richiede soluzioni affidabili.
                  Con nostra app l’utente puo trovare esperti di sicurezza informatica altamente qualificati per
                  proteggere i loro dati digitali e loro sistemi.
                </p>
                <h3 class="text-start title ms-3">Indice</h3>
                <div class="d-flex">
                  <div class="col-4 p-1 index-bg">
                    <h6 class="info">Analisi e Ricerca</h6>
                    <p class="description">Ricerca per comprendere il contesto dell’app .Qual è il suo scopo? Chi sono gli utenti target? Quali sono le esigenze degli utenti? 
                    </p>

                  </div>
                  <div class="col-4 p-1 index-bg">
                    <h6 class="info">Design</h6>
                    <p class="description">Un design pulito e organizzato per trasmettere un senso di sicurezza, professionalita e tecnologia.
                      </p>
                  </div>
                  <div class="col-4 p-1 index-bg">
                    <h6 class="info">Progetto</h6>
                    <p class="description">Utilizzo di Vue per il Frontend e Lravel per il Backend.</p>
                  </div>

                </div>

                <button class="btn me-4" @click="prevSlide">Indietro</button>
                <button class="btn" @click="nextSlide">Prossima Slide</button>

              </div>
              <!-- ---------slide-3----------- -->
              <div v-else-if="currentSlide === 3" class="slide col-10 " id="slide-3">
                <h2 class="title mt-5 mb-3 pt-5">Analisi Layout </h2>
                <p class="description mb-5">Layout organizzato e pulito che separa chiaramente <strong>la sezione sinistra</strong> , contenente una dettagliata descrizione della pagina, dalla <strong> parte destra</strong>, suddivisa in una <strong>navigazione</strong> strutturata e <strong>un'area principale</strong> contenente le funzionalità presentate attraverso eleganti <strong> card di Bootstrap</strong>.</p>
              <!--  -->
              <div class="container-fluid border border-secondary border-4">
                <div class="row">
                  <!-- Sidebar (col-4) -->
                  <!-- <div class="border-on-hover text-start" >la parte sinistra</div> -->
                  <div class="col-4 sidebar sinistra">
                    <!-- Contenuto della sidebar -->
                    <h5 class="mt-1">Sidbar</h5>
                    <p class="description"><strong>Dettagli Esplicativi della paggina.</strong></p>
                  </div>
              
                  <!-- Col-8 per Navbar e Main -->
                  
                  <div class="col-8 destra">
                    <!-- Navbar (row-1) -->
                    <div class="row bg-nav" style="height: 16%;" >
                      
                      <div class="col-12">
                        <!-- Contenuto della navbar -->
                        <div class="bordedestra-on-hover"> </div>
                        <h5 class="mt-1">NavBar </h5>
                    <p class="description"><strong>Accesso Rapido alle Sessioni.</strong> </p>
                      </div>
                    </div>
              
                    <!-- Main (row-2) -->
                    <div class="row bg-main" style="height: 85%;">
                      <div class="col-12 ">
                        <!-- Contenuto principale -->
                        <h5 class="mt-1">Main</h5>
                    <p class="description"><strong>Funzionalità Chiave mediante Carte di Bootstrap.</strong></p>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
              <!--  -->
                <button class="btn me-4 mt-5" @click="prevSlide">Indietro</button>
                <button class="btn mt-5" @click="nextSlide">Prossima Slide</button>
              </div>
              <!-- ------------slide-4 project--------- -->
              <div v-else-if="currentSlide === 4" class="slide col-10" id="slide-4">
                
                <div class="col-9">
                <h2 class="title mt-5 pt-4">Architettura del Progetto</h2>
                <p class="description">L'app è stata costruita con un <strong> backend</strong> robusto utilizzando <strong>Laravel</strong> , assicurando affidabilità e prestazioni ottimali. Per il <strong>frontend</strong> , abbiamo adottato <strong> Vue.js</strong>, garantendo un'interfaccia moderna e intuitiva per un'esperienza utente all'avanguardia.</p>
              </div>
                <!-- ----------- -->
                <h2 class="text-start  ms-3">Laravel: <span class="sottotitolo"> Il Cuore del Back-End</span></h2>
                <div class="d-flex">
                  <div class="col-4 p-1 index-bg">
                    <h6 class="info">Routes, Controllers, Models</h6>
                    <p class="description">Organizziamo la nostra logica di gestione delle richieste utilizzando Routes per definire le rotte, Controllers per gestire la logica, e Models per interagire con il database. 
                    </p>

                  </div>
                  <div class="col-4 p-1 index-bg">
                    <h6 class="info">Database Migrations e Seeders</h6>
                    <p class="description">Strutturiamo il nostro database in modo incrementale e gestibile con le migrations, mentre i seeders ci permettono di popolare il database con dati di esempio.
                      </p>
                  </div>

                </div>

                <h2 class="text-start ms-3">Vue JS: <span class="sottotitolo"> L'Arte del Front-End Interattivo</span></h2>
                <div class="d-flex">
                  <div class="col-4 p-1 index-bg">
                    <h6 class="info">Componenti Vue</h6>
                    <p class="description">Abbiamo abbracciato l'approccio modulare utilizzando i componenti Vue.js, che ci consentono di creare interfacce utente flessibili e riutilizzabili.
                    </p>

                  </div>
                  <div class="col-4 p-1 index-bg">
                    <h6 class="info">Vue Router</h6>
                    <p class="description"> La gestione della navigazione client-side con Vue Router, per migliorare l'esperienza utente senza dover ricaricare la pagina.
                      </p>
                  </div>


                </div>

                <!-- ----------- -->
                <div class="col-9">
                <button class="btn me-4" @click="prevSlide">Indietro</button>
                <button class="btn" @click="nextSlide">Prossima Slide</button>
              </div>
            </div>

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
  background-color: #202426;
  color: #fff;
  height: 100vh;
}

.presentation-right {
  background-image: url(/presentation-bg.jpg);
  background-attachment: fixed; //fissa il bg-img per evitare lo scrolling
  background-repeat: no-repeat;
  background-size: contain;
  background-position: right;
  height: 100vh;
}

.mar {
  margin-top: 32rem;
}

.info {
  font-size: 1rem;
  color: #1EBFCB;
  font-weight: bold
}

.title {
  font-size: 3rem;
  color: #1EBFCB;

}

.description {
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

/*--------------------------*/
/* stili per gli stili specifici di ciascuna slide  */
/* stili specifici per la prima slide-1 */
#slide-1 {

  .slide1-title {
    margin-top: 20rem;
    //margin-right: 12rem;
  }
}

/*------------------------------------*/
/* stili specifici per la prima slide-2 */
#slide-2 {

  .title {
    margin-top: 6rem;
    margin-bottom: 2rem;
  }

  .description {
    margin-bottom: 2rem;
  }

  .index-bg {
    height: 10rem;
    background-color: rgba(51, 51, 51, 0.5);
    border-left: 10px solid rgb(31, 192, 204, );
    ;
    border-radius: 10px;
    margin: 1rem;
  }
  .index-bg:hover {
    background-color:  rgba(51, 51, 51, 0.9);
  }

  .btn {
    margin-top: 3rem;
  }
}
/* stili specifici per la prima slide-3 */
#slide-3 {
  lef-part{
    background-color: #202426;
    color: #fff;
    height: 60vh;
  }
  .sidebar{
    background-color: rgba(61, 64, 66, 0.5);
    height: 25rem; 
    overflow: hidden;
    position: relative;
  }
  .sidebar:hover {
    background-color: rgba(61, 64, 66, 0.9);
  }
  .sidebar p{
    display: none;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
  
  }
  .sidebar:hover p{
    display: block;
  }
  .bg-nav{
    background-color: rgba(80, 103, 65, 0.5);
    overflow: hidden;
    position: relative;
  }
  .bg-nav:hover {
    background-color: rgba(80, 103, 65, 0.9);
  }
  .bg-nav p{
    display: none;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    
  }
  .bg-nav:hover p{
    display: block;
  }
  .bg-main{
    background-color: rgba(142, 90, 151, 0.5);
    overflow: hidden;
    position: relative;
  }
  .bg-main:hover {
    background-color: rgba(142, 90, 151, 0.9);
  }
  .bg-main p{
    display: none;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    
  }
  .bg-main:hover p{
    display: block;
  }
  h5{
    color: #1EBFCB;
  }


}
/*-----------slide-4 progetto-------*/
#slide-4{
  .title{
    margin-top: 1rem;
    margin-bottom: 0.5rem;
  }
  .description {
    margin-bottom: 1rem;
  }

  .index-bg {
    height: 10rem;
    background-color: rgba(51, 51, 51, 0.5);
    border-left: 10px solid rgb(31, 192, 204, );
    ;
    border-radius: 10px;
    margin: 1rem;
  }
  .index-bg:hover {
    background-color:  rgba(51, 51, 51, 0.9);
  }

  .btn {
    margin-top: 1rem;
  }
  .sottotitolo{
    font-size: 1.5rem;
    color: #b0b1b2;
  }
  h2{
    color: #1EBFCB;
    margin-top: 2rem;
  }
}

/*------------------------------------*/



</style>