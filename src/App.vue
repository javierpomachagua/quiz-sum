<template>
  <div class="container text-center">
    <h1>The Super Quiz</h1>
    <hr>
    <transition enter-active-class="animated rollIn" mode="out-in">
      <div class="panel panel-default" v-if="!correct">
        <div class="panel-heading">
          <b>What's {{ numberA }} + {{ numberB }}?</b>
        </div>
        <div class="panel-body">
          <div class="col-xs-6 col-md-6 col-lg-6" v-for="(result, index) in results" :key="index">
            <button class="btn btn-primary btn-lg btn-result" @click="check(result)">{{ result }}</button>
          </div>
        </div>
      </div>
    </transition>
    <transition enter-active-class="animated jackInTheBox" mode="out-in">
      <div class="panel panel-default" v-if="correct">
        <div class="panel-heading">
          <b>Result</b>
        </div>
        <div class="panel-body">
          <div class="alert alert-success">It's correct!</div>
          <button class="btn btn-primary" @click="newGame()">New Game</button>
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  data() {
    return {
      numberA: "",
      numberB: "",
      results: [],
      correct: false
    };
  },
  created() {
    this.newGame();
  },
  methods: {
    newGame() {
      this.correct = false;
      this.numberA = Math.floor(Math.random() * 100 + 1);
      this.numberB = Math.floor(Math.random() * 100 + 1);
      this.results = [];
      this.results.push(
        this.numberA + this.numberB,
        Math.floor(Math.random() * 100 + 1),
        Math.floor(Math.random() * 100 + 1),
        Math.floor(Math.random() * 100 + 1)
      );
      this.results.sort(() => {
        return 0.5 - Math.random();
      });
    },
    check(result) {
      if (this.numberA + this.numberB == result) {
        this.newGame();
        this.correct = true;
      } else {
        alert("Incorrect!");
      }
    }
  }
};
</script>

<style>
.btn-result {
  margin: 20px 20px;
}
</style>

