<template>
  <div class="content">
    <span>{{ label }}</span>
    <div class="selectWrapper">
      <select v-model="selectedCountry" :class="selectClass" @click="pushCities">
        <option disabled selected>{{ selectedCountry }}</option>
        <option v-for="country in countries"> {{ country.value }}</option>
      </select>
      <span v-if="selectClass === 'select notValid'">  — Выберите что-то</span>
      <select v-model="selectedCity" :class="selectClass">
        <option disabled selected>{{ selectedCity }}</option>
        <option v-for="city in cities"> {{ city.value }}</option>
      </select>
      <span v-if="selectClass === 'select notValid'"> — Выберите что-то</span>
    </div>
    <Btn
      v-for="btn in btns"
      :key="btn.id"
      :btn="btn"
      @getNext="getNext"
      @getPrev="getPrev"
    >
    </Btn>
  </div>
</template>

<script>
  import Btn from '../Btn.vue'
  import axios from 'axios'

  export default {
    components: {
      Btn
    },
    data() {
      return {
        information: {},
        label: '2. Выберите страну и город',
        selectedCountry: 'Страна',
        selectedCity: 'Выберите сначала страну',
        selectClass: 'select',
        countries: [],
        preCities: {},
        cities: [],
        btns: [
          {
            prev: 'Предыдущий',
            next: 'Следующий',
          }
        ]
      }
    },
    methods: {
      getNext() {
        if (this.selectedCountry !== 'Страна' && this.selectedCity !== 'Выберите сначала страну') {
          this.information['country'] = this.selectedCountry;
          this.information['city'] = this.selectedCity;
          this.$emit('getNext', this.information);
        } else {
          this.selectClass = 'select notValid';
        }
      },
      getPrev() {
        this.$emit('getPrev');
      },
      pushCities() {
        this.cities = [];
          for (let key in this.preCities) {
            if (this.preCities.hasOwnProperty(key)) {
              if (this.preCities[key].country === this.parseCountry(this.selectedCountry)) {
                this.cities.push({value: this.preCities[key].name});
              }
            }
          }
        if (this.cities.length === 0) {
          this.selectedCity = 'Страна не поддерживается';
        } else {
          this.selectedCity = 'Выберите город';
        }
      },
      parseCountry(country) {
        switch (country) {
          case "Ukraine":
            return 1;
          case "Germany":
            return 2;
          case "France":
            return 3;
          case "Spain":
            return 4;
          case "Sweden":
            return 5;
          case "USA":
            return 6;
          case "Canada":
            return 7;
          case "Moldova":
            return 8;
          case "Belarus":
            return 9;
          case "Poland":
            return 10;
        }
      }
    },
    mounted: function () {
      axios.get('src/assets/countries.json').then(response => {
        for (let key in response.data) {
          if (response.data.hasOwnProperty(key)) {
            this.countries.push({value: response.data[key]});
          }
        }
      });
      axios.get('src/assets/cities.json').then(response => {
        this.preCities = response.data;
      });
    }
  }
</script>

<style scoped>
  .selectWrapper {
    display: grid;
  }

  .select {
    font-family: "Open Sans", sans-serif;
    padding: 12px;
    margin-top: 16px;
    box-shadow: 0 1px 2px rgba(0, 0, 0, 0.2);
    border: 0;
    border-radius: 2px;
    width: 22em;
    background: #ffffff;
  }

  .select:after {
    color: #bbbbbb
  }

  select:disabled {
    font-family: "Open Sans", sans-serif;
    color: #bbbbbb;
    background: brown;
  }

  .content {
    margin: 16px auto;
  }

  .content span {
    margin-bottom: 24px;
    display: block;
  }

  .content .selectWrapper span {
    margin: -35px 0 0 300px;
    color: #ff0000;
  }

  .notValid {
    border: 1px solid #ff0000;
  }
</style>
