<template>
    <div class="container mt-4">
        <form v-on:submit="translateText(text,language)">
            <div class="form-group">
                <legend>Text</legend>
                <textarea class="form-control" rows="3" v-model="text"></textarea>
            </div>

            <div class="form-group">
              <legend>Select A Language </legend>
            <select class="form-control" v-model="language">
                  <option value="el">Greek</option>
                  <option value="es">Spanish</option>
                  <option value="fr">French</option>
                  <option value="zh">Chinese</option>
            </select>
            </div>
            <input class="btn btn-warning" type="submit" value="Translate">
        </form>
        <br>
    <div v-if="translatedText" class="card text-white bg-dark mb-3" style="max-width: 40rem;">
      <div class="card-header">Translation</div>
      <div class="card-body">
        <h2 class="card-text">{{translatedText}}</h2>
      </div>
    </div>
</div>
</template>

<script>

import axios from 'axios';
const API = YOUR_API_KEY;

export default {
    name: "Home",
    data() {
        return {
            translatedText: '',
            language: '',
            text: ''
        };
    },
    methods: {

        async translateText(text, language) {
            await axios.get(`${API}lang= ${language}&text=${text}`)
                .then(res =>
                    this.translatedText = res.data.text[0])
        }

    }
};
</script>
