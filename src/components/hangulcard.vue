<template>
  <div class="hangul-card">
    <h2>{{ msg }}</h2>

    <h2>{{ hangul }}</h2>

    <ul>
      <li v-for="letter in choices" v-bind:key="letter.roman" v-on:click="checkAnswer">
        {{ letter.roman }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'HangulCard',
  props: {
    msg: String,
    hangul: String,
    answer: String,
    choices: Array
  },
  methods: {
      checkAnswer: function(event) {
        if(event && event.srcElement.innerText === this.answer){
           this.$emit('optionSelected', true);
           return;
        }

        this.$emit('optionSelected', false);
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.hangul-card {
  display:flex;
  flex-direction: column;
  border: 1px solid;
  width: 30%;
  min-width: 300px;
}

.hangul-card.correct {
    border: 1px solid #00FF00;
}

.hangul-card.wrong {
    border: 1px solid #FF0000;
}

h3 {
  margin: 40px 0 0;
}
ul {
  display:flex;
  flex-wrap: wrap;
  align-items: center;
  align-content: center;
  justify-content: center;
  list-style-type: none;
  padding: 0;
}
li {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 10px 10px;
  border: 1px solid;
  width: 100px;
  height: 50px;
}

li:active{
  background-color: cornflowerblue;
}
a {
  color: #42b983;
}
</style>
