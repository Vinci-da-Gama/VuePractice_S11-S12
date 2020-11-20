const { for } = require("core-js/fn/symbol");

<template>
  <section>
    <base-card>
      <h2>Submitted Experiences</h2>
      <div>
        <base-button @click="loadUserExperience"
          >Load Submitted Experiences</base-button
        >
      </div>
      <p v-if="isLoading">Loading...</p>
      <p v-else-if="!isLoading && error"
        className="color-red">
        {{ error }}
      </p>
      <p v-else-if="!isLoading && (!results || results.length === 0)">
        No data in DB
      </p>
      <ul v-else>
        <survey-result
          v-for="result in results"
          :key="result.id"
          :name="result.name"
          :rating="result.rating"
        ></survey-result>
      </ul>
    </base-card>
  </section>
</template>

<script>
import SurveyResult from "./SurveyResult.vue";

export default {
  // props: ['results'],
  inject: ["baseUrl"],
  components: {
    SurveyResult,
  },
  data() {
    return {
      results: [],
      isLoading: false,
      error: null
    };
  },
  methods: {
    loadUserExperience() {
      this.isLoading = true;
      this.error = null;
      fetch(`${this.baseUrl}survey.json`)
        .then((resp) => {
          return resp.ok && resp.json();
        })
        .then((data) => {
          console.log("57 -- data: ", data);
          const rz = [];
          for(const id in data) {
            rz.push({
              id: id,
              name: data[id].name,
              rating: data[id].rating
            });
          }
          this.isLoading = false;
          this.results = rz;
        })
        .catch((err) => {
          this.isLoading = false;
          console.log(" 71 error -- ", err.message);
          this.error = err.message;
        });
    },
  },
  mounted () {
    this.loadUserExperience();
  },
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
</style>
