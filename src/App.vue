<template>
  <the-form></the-form>
  <learning-survey></learning-survey>
  <user-experiences></user-experiences>
</template>

<script>
import TheForm from './components/TheForm.vue';
// for section 12 -- http request
import LearningSurvey from './components/survey/LearningSurvey.vue';
import UserExperiences from './components/survey/UserExperiences.vue';

export default {
  components: {
    TheForm,
    LearningSurvey,
    UserExperiences
  },
  provide() {
    return {
      baseUrl: 'https://vue-http-demo-79c6e.firebaseio.com/'
    }
  },
  /* data() {
    return {
      savedSurveyResults: [],
    };
  },
  methods: {
    storeSurvey(surveyData) {
      const surveyResult = {
        name: surveyData.userName,
        rating: surveyData.rating,
        id: new Date().toISOString(),
      };
      this.savedSurveyResults.push(surveyResult);
      console.log(surveyResult);
    },
  } */
}
</script>

<style>
* {
  box-sizing: border-box;
}

html {
  font-family: sans-serif;
}

body {
  margin: 0;
  background-color: rgba(168, 168, 168, .5)
}
</style>