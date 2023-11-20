<template>
    <div class="row align-items-center">

        <div class=" col-md-6 offset-md-3">
            <div class="card shadow-sm p-3 mt-5 bg-body rounded">
                <div class="card-body">
                    <div class="input-group mb-3">
                        <input type="text" class="form-control" placeholder="Word" v-model="inputText">
                        <button class="btn btn-outline-primary" type="button" @click="getData(), visible=!visible">Button</button>
                    </div>
                </div>
            </div>

            <div class="card shadow-sm mt-3 bg-body rounded" v-if="visible">
                <div class="card-body" v-for="(mean, index) in word_meaning" :key="index">
                    <h3>{{ mean.partOfSpeech }}</h3>
                    <ul>
                        <li v-for="(definition, defIndex) in mean.definitions" :key="defIndex">
                            {{ definition.definition }}
                        </li>
                    </ul>
                </div>
            </div>
        </div>

    </div>

    
</template>
  
<script>
// import HelloWorld from './components/HelloWorld.vue'
import axios from 'axios';

export default {
    name: 'DictionaryApp',
    components: {
        // HelloWorld
    },
    data() {
        return {
            inputText: 'null',
            word_meaning: [],
            visible: false

        };
    },
    methods: {
        getData() {
            axios
                .get(`https://api.dictionaryapi.dev/api/v2/entries/en/${this.inputText}`)
                .then((result) => {

                    this.word_meaning = result.data[0].meanings;
                    // console.log(this.word_meaning);

                    // for (let i = 0; i < result.data[0].meanings.length; i++) {
                    //   // console.log('Part of Speech: ' + result.data[0].meanings[i].partOfSpeech);
                    //   this.part_of_speech = result.data[0].meanings[i].partOfSpeech;
                    //   console.log(this.part_of_speech);

                    //   for (let j = 0; j < result.data[0].meanings[i].definitions.length; j++) {
                    //     // console.log('Meaning: ' + result.data[0].meanings[i].definitions[j].definition);
                    //     this.word_meaning = result.data[0].meanings[i].definitions[j].definition;
                    //     console.log(this.word_meaning);
                    //     // this.res.push([this.part_of_speech, this.word_meaning])
                    //   }
                    // }

                })
                .catch((err) => {
                    console.error('API Error:', err);
                });
        }
    }
};

</script>

  