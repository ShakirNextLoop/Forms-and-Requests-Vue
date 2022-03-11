<template>
  <section>
    <base-card>
      <h2>Submitted Experiences</h2>
      <div>
        <base-button @click="loadResults"
          >Load Submitted Experiences</base-button
        >
      </div>
      <p v-if="isLoading">Loading</p>
      <ul>
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
import SurveyResult from './SurveyResult.vue';

export default {
  data() {
    return {
      results: [],
      isLoading: false,
    };
  },
  components: {
    SurveyResult,
  },
  methods: {
    loadResults() {
      this.isLoading=true
      fetch('https://firebase.url/surveys.json')
        .then((res) => {
          if (res.ok) {
            return res.json();
          }
        })
        .then((data) => {
          this.isLoading=false
          let results = [];
          for (const id in data) {
            results.push({
              id: id,
              name: data[id].userName,
              rating: data[id].rating,
            });
          }
          this.results = results;
        });
    },
  },
  mounted(){
    this.loadResults()
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