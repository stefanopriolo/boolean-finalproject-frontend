<template>
  <div class="rating">
    <span
      v-for="star in stars"
      :key="star"
      class="fa fa-star"
      :class="{ 'star-selected': star <= selectedScore || star <= hoverScore }"
      @click="selectStars(star)"
      @mouseenter="hoverStars(star)"
      @mouseleave="resetHover"
    ></span>
  </div>
</template>

<script>
export default {
  props: {
    initialScore: Number,
  },

  data() {
    return {
      stars: [1, 2, 3, 4, 5],
      selectedScore: 0,
      hoverScore: 0,
    };
  },

  methods: {
    hoverStars(score) {
      this.hoverScore = score;
    },
    selectStars(score) {
      this.selectedScore = score;
      this.$emit("update-score", score);
    },
    resetHover() {
      this.hoverScore = 0;
    },
  },
};
</script>

<style>
/* Aggiungi stili di base per le stelle */
.rating {
  font-size: 24px;
  color: #8f8f8f; /* Colore delle stelle vuote */
}

.fa-star {
  cursor: pointer;
  margin-right: 5px;
}

.star-selected {
  color: #fdcc0d; /* Colore delle stelle piene */
}
</style>
