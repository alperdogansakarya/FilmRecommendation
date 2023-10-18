<template>
  <div class="app">
    <h1>Ruh Halinizi Seçin</h1>

    <!-- Ruh hali seçeneklerini döngü ile listeleyin -->
    <label v-for="(moodOption, index) in moodOptions" :key="index">
      <input type="radio" v-model="selectedMood" :value="moodOption" />
      {{ moodOption }}
    </label>

    <!-- "Öneri Al" düğmesi -->
    <button @click="getMovieRecommendation">Öneri Al</button>

    <!-- Öneri sonucunu görüntülemek için bir alan -->
    <div class="recommendation" v-if="selectedMood && showRecommendation">
      <h2>Seçilen Ruh Hali: {{ selectedMood }}</h2>
      <p>Önerilen Film: {{ recommendedMovie }}</p>

      <!-- Ruh haline göre film resimleri -->
      <img v-if="selectedMood === 'Mutlu'" src="/truman.jpg" alt="Mutlu" />
      <img v-if="selectedMood === 'Uzgun'" src="/titanik.jpg" alt="Üzgün" />
      <img v-if="selectedMood === 'Sinirli'" src="/umut.jpg" alt="Sinirli" />
      <img v-if="selectedMood === 'Heyecanli'" src="/doktor.jpg" alt="Heyecanlı" />
      <img v-if="selectedMood === 'Hüzünlü'" src="/yesil.jpg" alt="Hüzünlü" />
    </div>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    const selectedMood = ref(null);
    const recommendedMovie = ref(null);
    const showRecommendation = ref(false);

    // Ruh hali seçenekleri
    const moodOptions = ["Mutlu", "Uzgun", "Sinirli", "Heyecanli", "Hüzünlü"];

    // "Öneri Al" düğmesine tıklandığında öneriyi al
    function getMovieRecommendation() {
      if (selectedMood.value) {
        recommendedMovie.value = movies[selectedMood.value];
        showRecommendation.value = true;
      } else {
        recommendedMovie.value = null;
        alert("Lütfen bir ruh hali seçiniz");
      }
    }

    // Ruh haline göre önerilen filmler
    const movies = {
      Mutlu: "Truman Show",
      Uzgun: "Titanik",
      Sinirli: "Umudunu Kaybetme",
      Heyecanli: "Doktor Strange",
      Hüzünlü: "Yeşil Yol",
    };

    return {
      selectedMood,
      recommendedMovie,
      getMovieRecommendation,
      moodOptions,
      showRecommendation,
    };
  },
};
</script>

<style scoped>
.app {
  background-color: #141414;
  color: #fff;
  text-align: center;
  padding: 20px;
}

label {
  display: block;
  margin: 10px;
  font-size: 18px;
}

input[type="radio"] {
  display: none;
}

input[type="radio"] + label::before {
  content: "";
  display: inline-block;
  width: 20px;
  height: 20px;
  margin-right: 5px;
  border: 2px solid #d32f2f;
  border-radius: 50%;
}

input[type="radio"]:checked + label::before {
  background-color: #d32f2f;
}

button {
  background-color: #d32f2f;
  color: #fff;
  padding: 10px 20px;
  font-size: 18px;
  border: none;
  cursor: pointer;
}

button:hover {
  background-color: #ff3d3d;
}

.recommendation {
  margin-top: 20px;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

img {
  max-width: 100%;
  max-height: 200px; /* Resimlerin maksimum yüksekliğini belirtin */
  margin: 10px;
}
</style>
