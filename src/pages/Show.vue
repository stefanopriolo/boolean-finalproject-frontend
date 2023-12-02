<script>
import axios from "axios";
import StarRating from "../components/StarRating.vue";

export default {
  components: {
    StarRating,
  },

  props: {
    initialScore: {
      type: Number,
      default: 0,
    },
  },
  data() {
    return {
      profile: {},
      user: {},

      formData: {
        name: "",
        surname: "",
        email: "",
        description: "",
        user_id: "",
      },

      errors: null,
      success: null,
      reviewSuccess: null,
      reviewName: "",
      reviewSurname: "",
      reviewText: "",
      reviewScore: this.initialScore,
      reviewSubmitted: false,
      reviewError: false,
    };
  },

  methods: {
    fetchData() {
      const userId = this.$route.params.id;

      axios
        .get(`http://127.0.0.1:8000/api/profile/${userId}`)
        .then((response) => {
          this.user = response.data.users.data[0];
          this.profile = response.data.profiles.data[0];
        })
        .catch((error) => {
          console.error("Error fetching data:", error);
        });
    },

    submitReview() {
      const userId = this.$route.params.id;

      axios
        .post(`http://127.0.0.1:8000/api/reviews`, {
          user_id: userId,
          name: this.reviewName,
          surname: this.reviewSurname,
          text: this.reviewText,
          score: this.reviewScore,
        })
        .then((response) => {
          this.reviewSuccess = "Recensione inviata con successo!";

          // Resetta i campi del form dopo l'invio
          this.reviewName = "";
          this.reviewSurname = "";
          this.reviewText = "";
          this.reviewScore = this.initialScore;
        })

        .catch((error) => {
          console.error("Error submitting review:", error.response);
          this.reviewError = true;
          this.reviewSuccess = null;
        });
    },

    getImageUrl(photo) {
      return `http://127.0.0.1:8000/storage/${photo}`;
    },

    onFormSubmit() {
      this.formData.user_id = this.profile.user_id;

      axios
        .post("http://localhost:8000/api/messages", this.formData)
        .then((response) => {
          this.success = response.data.message;
          this.errors = null;
        })
        .catch((error) => {
          this.errors = error.response?.data?.message ?? error.message;
        });
    },
    updateReviewScore(score) {
      this.reviewScore = score;
    },
  },

  mounted() {
    this.fetchData();
  },
};
</script>

<template>
  <div class="container home-style">
    <div class="row justify-content-between container-style">
      <div class="col-12 col-md-6">
        <div
          class="d-flex flex-column align-items-center text-center text-white"
        >
          <div class="container-photo-resize">
            <img
              v-if="profile.photo"
              :src="getImageUrl(profile.photo)"
              class="img-fluid rounded-circle photo-resize"
              alt="Profile Image"
            />
          </div>
          <h5 class="card-title">{{ user.name }} {{ user.surname }}</h5>
          <h4 class="bio-title pb-3" v-if="user.specializations">
            {{
              user.specializations
                .map((specialization) => specialization.name)
                .join(", ")
            }}
          </h4>
        </div>

        <div class="text-white pt-3 text-center">
          <h6 class="card-text bio-title">Email:</h6>
          <p>{{ user.email }}</p>

          <h6 class="card-text bio-title">Phone:</h6>
          <p>{{ profile.phone }}</p>
          <h6 class="card-text bio-title">Location:</h6>
          <p>{{ profile.location }}</p>
          <h6 class="card-text bio-title">Descrizione:</h6>
          <p>{{ profile.description }}</p>
          <router-link to="/" class="btn btn-info mt-3 mb-5"
            >Torna Indietro</router-link
          >
        </div>
      </div>

      <div class="col-12 col-md-4 text-white">
        <!-- SEZIONE MESSAGGI -->
        <h1>Contattami!</h1>

        <!-- messaggio errore -->
        <div class="alert alert-danger" v-if="errors">
          Sembra che tu non abbia compilato tutti i campi. Riprova!
        </div>

        <!-- form -->
        <form @submit.prevent="onFormSubmit" v-if="!success">
          <div class="mb-3">
            <label>Nome</label>
            <input type="text" class="form-control" v-model="formData.name" />
          </div>

          <div class="mb-3">
            <label>Cognome</label>
            <input
              type="text"
              class="form-control"
              v-model="formData.surname"
            />
          </div>

          <div class="mb-3">
            <label>Email</label>
            <input type="text" class="form-control" v-model="formData.email" />
          </div>

          <div class="mb-3">
            <label>Messaggio</label>
            <textarea
              class="form-control"
              v-model="formData.description"
            ></textarea>
          </div>

          <button type="submit" class="btn btn-primary mb-3">Invia</button>
        </form>

        <!-- messaggio invio SE a buon fine -->
        <div class="alert alert-success" v-else>{{ this.success }}</div>

        <h1 class="pt-5">Scrivimi una recensione!</h1>

        <!-- Form recensione: -->
        <form @submit.prevent="submitReview" v-if="!reviewSuccess">
          <div class="mb-3">
            <label for="score" class="form-label">Voto:</label>
            <star-rating
              :initial-score="reviewScore"
              @update-score="updateReviewScore"
              ref="starRating"
            />
          </div>
          <div class="mb-3">
            <label for="name" class="form-label">Nome:</label>
            <input
              type="text"
              v-model="reviewName"
              class="form-control"
              required
            />
          </div>

          <div class="mb-3">
            <label for="surname" class="form-label">Cognome:</label>
            <input
              type="text"
              v-model="reviewSurname"
              class="form-control"
              required
            />
          </div>

          <div class="mb-3">
            <label for="text" class="form-label">Recensione:</label>
            <textarea
              v-model="reviewText"
              class="form-control"
              required
            ></textarea>
          </div>

          <button type="submit" class="btn btn-primary mb-5">
            Invia Recensione
          </button>
        </form>

        <!-- Messaggio di conferma o errore -->
        <div class="alert alert-success" v-else>{{ this.reviewSuccess }}</div>

        <div v-if="reviewError">
          <p class="mt-3 text-danger">
            Si è verificato un errore durante l'invio della recensione.
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>

.home-style{

padding-top: 85px;
height: 100vh;
}
.container-style{
  background-color: rgba(51, 51, 51, 0.6);
  padding: 50px;
  border-radius: 50px;
}
.btn {
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
.container-photo-resize {
  aspect-ratio: 1 / 1;
  width: 100%;
  max-width: 20rem;
  overflow: hidden;
}

.photo-resize {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.card-title {
  font-size: 2.5em;
  margin-bottom: 10px;
}

.card-text {
  margin-bottom: 8px;
}

/* Aggiunti stili per il componente StarRating */
.rating {
  font-size: 1.25rem;
  /* Imposta la dimensione del font delle stelle */
}

.stars-container {
  color: #ffc107;
  /* Colore delle stelle vuote */
}

.star {
  cursor: pointer;
}

.star.selected {
  color: #fdcc0d;
  /* Colore delle stelle piene */
}

.bio-title {
  color: #27cdf2;
}
</style>
