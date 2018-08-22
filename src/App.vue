<template>
  <div id="app">
    <img src="./assets/logo.png">
    <h1>Multiple Choice</h1>
    <h2>Game</h2>
    <div class="game-mc">
      <div class="game-mc__box">
        <div class="game-mc__box__media">
          <img src="https://s3-us-west-2.amazonaws.com/courses-images/wp-content/uploads/sites/110/2016/05/02161121/biodiversity_examples.jpg">
        </div>
        <div class="game-mc__box__question">

        </div>
      </div>
      <div class="game-mc__options">
        <button v-if="!ended" :disabled="!question.answered">Next</button>
        <button v-else>Finish</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      question: {
        answered: false
      },
      ended: false,
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

.game-mc {
  &, & div {
    border: 2px solid black;
  }
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-content: stretch;
  align-items: stretch;
  flex-direction: column;
  &__box {
    flex-basis: calc(90% - 10px);
    display: flex;
    padding: 5px 15px;
    &__media {
      flex-basis: 50%;
      padding-right: 20px;
      img {
        height: 100%;
        width: 100%;
      }
    }
    &__question {
      flex-basis: 50%;
      padding-left: 20px;
    }
  }
  &__options {
    flex-basis: calc(10% - 10px);
    padding: 5px 10px;
    text-align: right;
    button {
      padding: 10px 25px;
      font-size: 16px;
      border-radius: 25px;
      border: 2px solid transparent;
    }
  }
}
</style>
