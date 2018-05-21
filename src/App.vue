<template>
  <div id="app">
    <!--<link href="https://cdn.jsdelivr.net/npm/animate.css@3.5.1" rel="stylesheet" type="text/css">-->
    <!--<img src="./assets/logo.png">-->

    <h1>Welcome to Hangul Quiz</h1>

    <HangulCard id="hangulcard" @optionSelected="handleOption" :msg="message" :hangul="hangul" :answer="answer" v-bind:choices="choices"
      v-bind:class="{ 'correct': correctAnswer, 'wrong': wrongAnswer, 'animated flipInY': show, 'animated flipOutY': hide}"/>

    <div>
      Correct {{correct}} - Incorrect {{incorrect}}
    </div>
  </div>
</template>

<script>
import HangulCard from './components/hangulcard.vue'

export default {
  name: 'app',
  components: {
    HangulCard
  },
  data: function(){
    return {
      allHangul:    ['ㅏ','ㅐ','ㅑ','ㅒ','ㅓ','ㅔ','ㅕ','ㅖ','ㅗ','ㅘ','ㅙ','ㅚ','ㅛ','ㅜ','ㅝ','ㅞ','ㅟ','ㅠ','ㅡ','ㅢ','ㅣ','ㄱ','ㄲ','ㄴ','ㄷ','ㄸ','ㄹ','ㅁ','ㅂ','ㅃ','ㅅ','ㅆ','ㅇ','ㅈ','ㅉ','ㅊ','ㅋ','ㅌ','ㅍ'	,'ㅎ'],
      allRomanized: ['a','ae','ya','yae','eo','e','yeo','ye','o','wa','wae','oe','yo','u','wo','we','wi','yu','eu','ui','i','g','kk','n','d','tt','r','m','b','pp','s','ss','(silent)','j','jj','ch','k','t','p','h'],
      message: "Next Question",
      answer: "",
      choices: [],
      hangul: "",
      correct: 0,
      incorrect: 0,
      correctAnswer: false,
      wrongAnswer: false,
      show: false,
      hide: false
    }
  },
  methods:{
      newCard: function(){
          var randomAnswer = Math.floor(Math.random()*4);
          this.choices = this.getRandomChoices(this.answer);
          this.answer = this.choices[randomAnswer].roman;
          this.hangul = this.choices[randomAnswer].hangul;
          this.correctAnswer = false;
          this.wrongAnswer = false;
          this.hide = false;
          this.show = true;
      },
      getRandomChoices: function(){
          var choices = [];
          var randomIndex = this.randomIndex();
          for(var i=0;i<4;i++){
              randomIndex = this.randomIndex();
              choices.push({roman:this.allRomanized[randomIndex], hangul: this.allHangul[randomIndex]});
              console.log(randomIndex);
          }
          return choices;
      },
      randomIndex: function(){
          var level = Math.floor(this.correct / 5)+5;
          return Math.floor(
              Math.random()*level
          );
      },
      handleOption: function(event){
          console.log('event option ', event);
          if(event == true){
              this.correct++;
              this.correctAnswer = true;
          }else{
              this.incorrect++;
              this.wrongAnswer = true;
          }
          this.show = false;
          this.hide = true;
          this.showCard();
      },
      showCard: function(){
          setTimeout(this.newCard, 1000);
      }
  },
  created: function(){
      var randomIndex = this.randomIndex();
      var randomAnswer = Math.floor(Math.random()*4);
      this.choices = this.getRandomChoices(this.answer);
      this.answer = this.choices[randomAnswer].roman;
      this.hangul = this.choices[randomAnswer].hangul;
      this.show = true;
      console.log(randomIndex,this.answer,this.hangul);
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
