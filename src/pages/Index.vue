<script>
import axios from "axios";

export default {
  data() {
    return {
      specializationNames:{
        1: 'Security specialist',
        2: 'Vulnerability assessor',
        3: 'Security administrator',
        4: 'Cryptographer',
        5:"Security manager",
        6:"Security analyst",
        8:"Security architect",
        9:"Malware analyst",
        10:"Consulente di Sicurezza",
        11:"Security consultant",
        12:"Security engineer",
        13:"Chief Information Security Officer, CISO)",
      },
      profiles: [],
      average_score: 0,
      specializations: [],
      minAverageScore: 0,
      specializationId: 0,
      minReviewCount: 0,
    };
  },
  methods: {
    async fetchDataProfile() {
      this.profiles = await this.fetchUsersBySpecialization();
    },

    async fetchUsersBySpecialization() {
      const apiUrlSpecialization = this.specializationId
        ? `http://127.0.0.1:8000/api/users/specialization/${this.specializationId}`
        : null;

      try {
        if (apiUrlSpecialization) {
          const response = await axios.get(apiUrlSpecialization);
          return response.data.data;
        }
      } catch (error) {
        console.error(
          "Errore durante il recupero dei dati di specializzazione:",
          error
        );
      }
    },

    getImageUrl(photo) {
      return `http://127.0.0.1:8000/storage/${photo}`;
    },

    displayStars(averageScore) {
      const roundedScore = Math.round(averageScore);
      const starCount = 5;

      // Creiamo una stringa di stelle basata sulla media dei voti utilizzando le icone di Font Awesome
      const fullStar = '<i class="fas fa-star" style="color: #fdcc0d;"></i>';
      const emptyStar = '<i class="far fa-star" style="color: #fdcc0d;"></i>';
      const stars =
        fullStar.repeat(roundedScore) +
        emptyStar.repeat(starCount - roundedScore);

      return `<span class="fa-stack fa-lg" style="display: flex; gap: 0.2rem; width:100%">${stars}</span>`;
    },
  },

  mounted() {
    this.specializationId = this.$route.params.specialization;
    this.fetchDataProfile();
  },
};
</script>

<template>
  <div class="container-fluid h-100 home-style">
    <div class="row h-100">
      <div class="col-12 col-lg-4 categories-bg text-center">
        <div class="header">
          <strong>
            <h1 class="title">Cerca il tuo esperto</h1>
          </strong>

          <p class="description ps-5 pe-5">
            Cerca il tuo esperto di sicurezza informatica tra i professionisti altamente qualificati di Cyber Security.
            Utilizza i filtri seguenti per personalizzare la tua ricerca:

            <strong> <br>Filtra per Media Voti:</strong> Seleziona il punteggio minimo che desideri per gli esperti. Puoi
            scegliere tra 1 e 5 stelle.

            <strong><br>Filtra per Numero di Recensioni:</strong> Indica il numero minimo di recensioni che gli esperti
            devono avere. Puoi selezionare tra 1, 5, e 10 recensioni.

            Una volta applicati i filtri, scorri le card degli esperti di sicurezza per trovare il professionista che
            meglio soddisfa le tue esigenze digitali. La tua sicurezza online è la nostra priorità.
          </p>
        </div>
        <div class="row flex-column justify-content-center p-5 ">
          <div class="col-4 pb-3 w-100 select-style">
            <label for="minAverageScore" class="form-label">Seleziona Media Voti:</label>
            <select v-model="minAverageScore" @change="fetchDataProfile" class="form-select">
              <option value="0">Mostra tutti</option>
              <option v-for="score in [1, 2, 3, 4, 5]" :key="score" :value="score">
                {{ score }} {{ score === 5 ? '' : '+' }}
              </option>
            </select>
          </div>
          <div class="col-4 w-100 select-style">
            <label for="numeroRecensioni" class="form-label">Seleziona utenti con più di:</label>
            <select v-model="minReviewCount" @change="fetchDataProfile" class="form-select">
              <option value="0">Mostra tutti</option>
              <option v-for="count in [1, 5, 10]" :key="count" :value="count">
                {{ count }} {{ count === 1 ? 'recensione' : 'recensioni' }}
              </option>
            </select>
          </div>
        </div>
        <router-link to="/" class="btn btn-primary">Torna Indietro</router-link>

      </div>


      <div class="col-lg-8 col-12">
        <div class="row pt-4">
          <div class="col-6"></div>

          <div class="col-5">
            <div class="header text-center">
              <h2 class="slogan text-end">Esperti di Sicurezza</h2>
              <h4 class="slogan-font-color text-end mb-5 fs-3">
                {{ specializationNames[specializationId] }}
              </h4>
            </div>
          </div>
        </div>

        <!-- bootstrap card -->

        <!-- Visualizza le card degli utenti -->
        <div class="row row-cols-auto gy-5 scrolling-container">
          <div class="col col-style" v-for="user in profiles" :key="user.id">
            <div class="card bg-card" style="width: 18rem; height: 100%" v-if="!isNaN(user.average_score) &&
              user.average_score >= minAverageScore &&
              !isNaN(user.review_count) &&
              user.review_count >= minReviewCount
              ">
              <img style="height: 18rem; object-fit: cover" v-if="user.profile && user.profile.photo"
                :src="getImageUrl(user.profile.photo)" class="card-img-top" alt="Immagine Professionista" />

              <div class="blue-site card-body flex-column" v-if="user.profile">
                <h3 class="">{{ user.name }} {{ user.surname }}</h3>
                <div class="text-center d-flex">
                  <span v-html="displayStars(user.average_score)"></span>
                  <span class="review-count description ps-4">({{ user.review_count || 0 }})</span>
                </div>
                <p class="blue-site">
                  Location:
                  <span class="description">{{ user.profile.location }} </span>
                </p>
                <p class="blue-site" style="word-wrap: break-word">
                  Descrizione:
                  <span class="description">
                    {{ user.profile.description && user.profile.description.length > 50 ?
                      user.profile.description.slice(0, 50) +
                      '...' : user.profile.description }}</span>
                </p>
                <p class="blue-site">Specialization:</p>
                <ul>
                  <li class="description" v-html="user.specializations
                    .map((specialization) => specialization.name)
                    .join('<br />')
                    "></li>
                </ul>
                <div class="mb-3 text-center">
                  <router-link class="btn btn-primary"
                    :to="{ name: 'show', params: { id: user.id } }">Dettagli</router-link>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- -------------------------------- -->
    </div>
  </div>

  <!-- ------------------------------ -->
</template>

<style lang="scss" scoped>
.home-style {

  padding-top: 85px;
}

.info {
  font-size: 1rem;
  font-weight: bold;
}

.blue-site {
  color: #27cdf2;
}

body {
  background-image: url(/bg-2.jpg);
  background-size: cover;
  background-attachment: fixed; //fissa il bg-img per evitare lo scrolling
  background-repeat: no-repeat;
}

/* aggiunge un overlay trasparente all'immagine di sfondo */
// body::before {
//   content: "";
//   background: rgba(173, 171, 171, 0.5);
//   position: fixed;
//   top: 0;
//   left: 0;
//   width: 100%;
//   height: 100%;
//   z-index: -1;
//   /* Posiziona l'overlay dietro all'immagine di sfondo */
// }
.select-style select {
  color: white;
  background-color: #27cdf236;
}

.select-style select option {
  color: black;
  background-color: rgba(39, 205, 242, 0.1215686275);
  ;
}



.categories-bg {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);

  border-top-right-radius: 40px;
  background-color: rgba(51, 51, 51, 0.6);
  color: #fff;
}

/* ----------------------------------------- */
.title {
  font-size: 4rem;
  color: #27cdf2;
}

.description {
  //color: white;
  color: #b0b1b2;
}

.slogan {
  color: #27cdf2;
  margin-bottom: 0;
}

.slogan h4 {
  margin-top: -1.5rem;
}

.slogan-font-color {
  color: #b0b1b2;
}

.btn {
  --bs-btn-border-color: #27cdf2;
  cursor: pointer;
  background-color: rgb(37, 37, 37);
  color: #27cdf2;
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

.col-style {
  display: flex;
  justify-content: space-between;
}

/*----- Stile per il contenitore con uno scroll orizzontale -------*/
.scrolling-container {
  padding: 1rem 0 0 2rem;
  white-space: nowrap;
  /* Evita che le card si spezzino su più righe */
}

.bg-card {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);

  background-color: rgba(51, 51, 51, 0.5);
  color: #b0b1b2;
}

.card-body {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  overflow: hidden;
  white-space: pre-wrap;
}

.link {
  color: #27cdf2;
}

img {
  width: 100%;
}


/* @media screen and (max-width:967px) {
.col-style{
  justify-content: center;
}
} */

@media screen and (max-width:623px) {
  .categories-bg {
    padding-bottom: 10px;
  }

  .scrolling-container {
    padding: 0 0 20px 0;
    display: flex;
    justify-content: center;
  }
}
</style>
