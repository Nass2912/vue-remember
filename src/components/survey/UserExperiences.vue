<template>
  <section>
    <base-card>
      <h2>Submitted Experiences</h2>
      <div>
        <base-button @click="fetchDatasss"
          >Load Submitted Experiences</base-button
        >
      </div>
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
  components: {
    SurveyResult,
  },

  data() {
    return {
      results: [],
    };
  },

  methods: {
    async fetchDatasss() {
      let fetcher = await fetch(
        'https://vue-http-6cee4-default-rtdb.firebaseio.com/surveys.json'
      );
      let fetched = await fetcher.json();
      for (const id in fetched) {
        this.results.push({
          id: id,
          name: fetched[id].userName,
          rating: fetched[id].rating,
        });
      }
    },
  },
  mounted() {
    console.log('sadasd');
    this.fetchDatasss();
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
