<template>
  <div id="app">
    <header>
      <h1>Beatles Ipsum</h1>
    </header>
    <div class="ipsum-options">
      <form @submit.prevent="generateIpsum">
        <div>
          <label for="paragraphs">Number of Paragraphs:</label>
          <input id="paragraphs" type="number" v-model="paragraphs">
        </div>
        <button>Generate Ipsum</button>
      </form>
    </div>
    <template v-if="showIpsum">
        <div class="ipsum-results" ref="ipsum" v-html="generateParagraphs()">
      </div>
    </template>
  </div>
</template>

<script>
import {phrases} from './data/phrases';

export default {
  name: 'App',
  data() {
    return {
      phrases,
      paragraphs: 6,
      showIpsum: false,
      sentenceLengthMin: 10,
      sentenceLengthMax: 14,
    }
  },
  methods: {
    getRandomPhrase() {
      return this.phrases[Math.floor(Math.random() * this.phrases.length)]
    },
    generateRandomSentence() {
      let words = '';
      let paragraph = '';
      const numSentences = 4;
      const sentenceLength = Math.floor(Math.random() * (this.sentenceLengthMax - this.sentenceLengthMin) + this.sentenceLengthMin);


      for(let i = 1; i < sentenceLength; i++) {
        words += this.getRandomPhrase() + ' ';
      }

      words = words.charAt(0).toUpperCase() + words.slice(1)

      for(let i = 1; i < (Math.floor(Math.random() * numSentences) + 2); i ++) {
        paragraph += (words.trim().endsWith('?') ? words.trim() : words.trim() + '. ')
      }

      return paragraph;

    },
    generateParagraphs() {
      let paragraphs = '';
      for(let i = 0; i < this.paragraphs; i++) {
        paragraphs += '<p>' + this.generateRandomSentence() + '</p>';
      }

      return paragraphs;
    },
    generateIpsum() {
      this.showIpsum = false
      this.showIpsum = true
    },
  },
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Open+Sans&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Limelight&display=swap');

body {
  min-width: 100vw;
  min-height: 100vh;
  margin:0;
  padding:0;
  box-sizing: border-box;
  display: flex;
  justify-content: center;
  font-family: 'Open Sans', sans-serif;
  background:#000;
  color: #fff;
}

header {
  width:100%;
  text-align: center;
  color:#000;
  margin-bottom: 24px;
  padding: 35px 24px;
  color: #fff;
  box-sizing: border-box;
}

header h1 {
  font-size: 5em;
  font-family: 'Limelight', cursive;
}

#app {
  background:#000;
}

header {
  width:100%;
  text-align: center;
  color:#fff;
  margin-bottom: 24px;
}

#app {
  background: #000;
  width:100%;
  box-sizing: border-box;
  display: flex;
  flex-direction: column;
  align-items: center;
}

button {
  font-size: inherit;
  font-family: inherit;
  border: none;
  padding: 12px 24px;
  cursor: pointer;
  background: #fff;
  color:#000;
  background: #fff;
  display: block;
  margin-top: 35px;
}

label {
  margin-right: 30px;
}

.ipsum-options {
  width: 100%;
  box-sizing: border-box;
  padding: 24px;
}

input {
  font-size: inherit;
}

.ipsum-options form {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100%;
}

.ipsum-results {
  padding: 24px;
  box-sizing: border-box;
  width: 100%;
  max-width: 960px;
}
</style>
