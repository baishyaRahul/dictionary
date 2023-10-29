<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <div id="app">

    <input v-model="inputText" type="text" placeholder="Enter text">
    <button @click="getData()">Meaning</button>
    <!-- <p v-if="word_noun">Part of Speech: {{ word_noun }}</p> -->
    <!-- <p v-for="( meaning, j ) in word_meaning" :key="j">Part of Speech: {{ meaning.definition }}</p> -->
    
    <p v-for="( speech, i ) in part_of_speech" :key="i">{{ i + 1 }}. {{ speech.partOfSpeech }}</p>
    <p > {{ part_of_speech }}</p>


  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import axios from 'axios';

export default {
  name: 'App',
  components: {
    // HelloWorld
  },
  data() {
    return {
      inputText: 'null',
      word_meaning: [],
      part_of_speech: []
    };
  },
  methods: {
    getData() {
      axios
        .get(`https://api.dictionaryapi.dev/api/v2/entries/en/${this.inputText}`)
        .then((result) => {

          // this.word_noun = result.data[0].meanings.partOfSpeech;
          // this.word_meaning = result.data[0].meanings.definitions.definition;
          // console.log(result.data[0].meanings);

          for (let i = 0; i < result.data[0].meanings.length; i++) {
            console.log('Part of Speech: ' + result.data[0].meanings[i].partOfSpeech);
            this.part_of_speech = result.data[0].meanings[i].partOfSpeech;
            for (let j = 0; j < result.data[0].meanings[i].definitions.length; j++) {
              console.log(result.data[0].meanings[i].definitions[j].definition);
              this.word_meaning = result.data[0].meanings[i].definitions[j].definition;
            }

          }
        })
        .catch((err) => {
          console.error('API Error:', err);
        });
    }
  }
};

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
