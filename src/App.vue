<template>
  <!-- warunkow deklaracja klasy, wrapper jest teraz zwykłą domyślną klasą (tablica klas []) -->
  <div :class="[{flexStart: step === 1}, 'wrapper']">
    <transition name="slide">
       <img src="./assets/logo.svg" class="logo" v-if="step === 1">
    </transition>
    <transition name="fade">
       <HeroImage v-if="step === 0"/>
    </transition>
    <Claim v-if="step === 0"/>
    <SearchInput v-model="searchValue" @input="handleInput" :dark="step === 1"/>
    <div class="results" v-if="results && !loading && step === 1">
      <ResultsItem v-for="item in results" :item="item" :key="item.data[0].nasa_id" />
    </div>
  </div>
</template>
<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim.vue';
import SearchInput from '@/components/SearchInput.vue';
import HeroImage from '@/components/HeroImage.vue';
import ResultsItem from '@/components/ResultsItem.vue';

const API = 'https://images-api.nasa.gov/search';

export default {
  name: 'Search',
  components: {
    Claim,
    ResultsItem,
    SearchInput,
    HeroImage,
  },
  data() {
    return {
      loading: false,
      step: 0,
      searchValue: '',
      results: [],
    };
  },
  methods: {
    handleInput: debounce(function search() {
      this.loading = true;
      console.log(this.searchValue);
      axios.get(`${API}?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          this.results = response.data.collection.items;
          this.loading = false;
          this.step = 1;
        })
        .catch((error) => {
          console.log('error: ', error);
        });
    }, 500),
  },
};
</script>
<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=Montserrat:300,400,600,800&display=swap');

  * {
    box-sizing: border-box;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  body {
    font-family: Montserrat, sans-serif;
    padding: 0;
    margin: 0;
  }

  .wrapper {
    position: relative;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    margin: 0;
    padding: 30px;
    width: 100%;
    min-height: 100vh;

    &.flexStart {
      justify-content: flex-start;
    }
  }

  .logo {
    position: absolute;
    top: 30px;
  }

  .results {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 20px;

    @media (min-width: 768px) {
      grid-template-columns: 1fr 1fr 1fr;
    }
  }

  // ANIMATIONS
  .fade-enter-active, .fade-leave-active {
    transition: opacity .4s ease;
  }
  .fade-enter, .fade-leave-to {
    opacity: 0;
  }

  .slide-enter-active, .slide-leave-active {
    transition: margin-top .4s ease;
  }
  .slide-enter, .slide-leave-to {
    margin-top: -50px;
  }
</style>
