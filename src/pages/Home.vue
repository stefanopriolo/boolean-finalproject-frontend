<script>
import axios from "axios";

export default {
  data() {
    return {
      currentIndex: 0,
      itemWidth: 18,
      specializations: [],
      selectedSpecialization: null,
      premiumUsers: [], // Array per i dati degli utenti "premium"
    };
  },
  methods: {
    getSpecializationsFromApi() {
      axios.get("http://127.0.0.1:8000/api/specialization").then((response) => {
        this.specializations = response.data;
      });
    },

    selectSpecialization(specializationId) {
      this.$router.push({
        name: "index",
        params: { specialization: specializationId },
      });
    },

    showDescription(specialization) {
      this.selectedSpecialization = specialization;
    },

    getPremiumUsersFromApi() {
      axios.get("http://127.0.0.1:8000/api/premium-users").then((response) => {
        this.premiumUsers = response.data;
      });
    },

    getImageUrl(photo) {
      return `http://127.0.0.1:8000/storage/${photo}`;
    },

    slide(direction) {
      const totalItems = this.premiumUsers.length;

      if (direction === 'left') {
        this.currentIndex = (this.currentIndex - 1 + totalItems) % totalItems;
        if (this.currentIndex === totalItems - 1) {
          this.currentIndex = 0;
        }
      } else if (direction === 'right') {
        this.currentIndex = (this.currentIndex + 1) % totalItems;
        // Correggi l'operatore di assegnazione qui
        if (this.currentIndex === totalItems - 1) {
          this.currentIndex = 0;
        }
      }



      const wrapper = this.$refs.sliderContainer;
      wrapper.style.transform = `translateX(-${this.currentIndex * this.itemWidth}rem)`;
    }



  },

  mounted() {
    this.getSpecializationsFromApi();
    this.getPremiumUsersFromApi();
  },
};
</script>

<template>
  <div class="container-fluid m-0 home-style">
    <div class="row h-100">
      <div class="col-lg-5 col-12 text-center categories-bg">
        <strong>
          <h1 class="title">Cyber Security</h1>
        </strong>

        <p class="description ps-5 pe-5">
          La tua sicurezza informatica è fondamentale. Scopri esperti
          specializzati, leggi recensioni e richiedi consulenza con Cyber
          Security. Proteggi il tuo mondo digitale con noi.
        </p>

        <div class="text-center mt-5">
          <h5 class="title-cat-color">Cerca la Specializzazione Desiderata</h5>
        </div>
        <div class="text-center">
          <div class="text-center">
            <i class="fa-solid fa-chevron-up"></i>
          </div>
          <div v-for="(specialization, index) in specializations" :key="index"
            @click="selectSpecialization(specialization?.id)" @mouseover="showDescription(specialization)"
            @mouseout="selectedSpecialization = null" class="badge-style btn btn-primary">
            {{ specialization?.name }}
          </div>
          <div class="prev-arrow text-center">
            <i class="fa-solid fa-chevron-down"></i>
          </div>
        </div>

        <!-- descrizione catergorie  -->
        <div class="description-tooltip pb-5 pt-5" v-if="selectedSpecialization">
          {{ selectedSpecialization.description }}
        </div>
      </div>
      <!-- Contenuto delle categorie -->

      <!-- ------------------------------ -->

      <!-- Stampa le card degli utenti che hanno una sponsorizzazione attiva -->

      <div class="col-lg-7 col-12 pt-5" style="padding-right:50px; position: relative;">
        <h2 class="slogan text-end">Sicurezza Digitale su Misura</h2>
        <h4 class="slogan-font-color text-end mb-5">Esperti in evidenza:</h4>


        <div class="slider-container">
          <div class="slider-wrapper" ref="sliderContainer">
            <div v-for="user in premiumUsers" :key="user.id" class="slider-item">
              <div class="card bg-card" style="width: 18rem; height: 100%">
                <img :src="getImageUrl(user.profile.photo)" class="card-img-top mb-2" alt="Immagine dell'utente"
                  style="height: 15rem; object-fit: cover" />
                  <i class="fa-solid fa-crown text-warning"></i>
                <div class="card-body flex-column">
                  <h3 class="card-title py-2 blue-site">
                    {{ user.name }} {{ user.surname }}
                  </h3>
                  <h6 class="card-subtitle mb-2">Specializzazioni:</h6>
                  <ul>
                    <li class="blue-site" v-for="specialization in user.specializations" :key="specialization.id">
                      {{ specialization.name }}
                    </li>
                  </ul>
                  <p class="card-text"> {{ user.profile.description && user.profile.description.length > 50 ?
                    user.profile.description.slice(0, 50) +
                    '...' : user.profile.description }}</p>
                  <router-link class="btn btn-primary"
                    :to="{ name: 'show', params: { id: user.id } }">Dettagli</router-link>
                </div>
              </div>
            </div>

          </div>
          <button class="slider-arrow left" @click="slide('left')">&lt;</button>
          <button class="slider-arrow right" @click="slide('right')">&gt;</button>

        </div>





      </div>
    </div>
  </div>
  <!-- -------------------------------- -->
</template>

<style lang="scss" scoped>
.home-style{

  padding-top: 85px;
  height: 100vh;
}

.blue-site {
  color: #27cdf2;
}

.description-tooltip {
  color: #b0b1b2;
}

.card-height {
  height: 35rem;
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

.title {
  font-size: 4rem;
  color: #27cdf2;
}

.description {
  //color: white;
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

/*----- Stile per il contenitore con uno scroll orizzontale -------*/
.scrolling-container {
  white-space: nowrap;
  /* Evita che le card si spezzino su più righe */
  overflow-x: auto;
  white-space: nowrap;
  margin-top: 22rem;
  margin-left: 2rem;
}

.bg-card {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
  position: relative;
  background-color: rgba(51, 51, 51, 0.6);
  color: #b0b1b2;

  i{
    position: absolute;
    font-size: 1.5rem;
    padding: 10px;
    width: 100%;
    background-color: rgba(0, 0, 0, 0.246);
    box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);

  }
}

/*----------------------*/
.categories-bg {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
  border-top-right-radius: 40px;
  background-color: rgba(51, 51, 51, 0.6);
  color: #fff;
}

.title-cat-color {
  color: #b0b1b2;
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
  color: #b0b1b2;
}

.card-body {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  overflow: hidden;
  white-space: pre-wrap;
}

.slider-container {
  padding: 1rem 2rem;
  overflow: hidden;

}

.slider-wrapper {
  transition: transform 0.5s ease-in-out;

  display: flex;
}

.slider-item {
  flex: 0 0 18rem;
  margin-right: 20px; // Aggiungi uno spazio tra gli elementi

}

.slider-arrow {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  font-size: 20px;
  background: transparent;
  border: none;
  cursor: pointer;
  color: #fff;
}

.left {
  font-size: 2rem;
  left: 10px;
}

.right {
  font-size: 2rem;

  right: 10px;
}


@media screen and (min-width:1850px) {
  .categories-bg {
    max-width: 850px;
  }
}



/* Stile per posizionare la descrizione delle categorie al centro */

/*-----------------------------------------------*/
</style>
