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
          <div class="game-mc__box__question__text">
            <span>{{ question.question }}</span>
          </div>
          <div class="game-mc__box__question__answers">
            <div v-for="(aswr, index) in question.answers" class="game-mc__box__question__answers__item"
                 :class="{
                   right: (question.answered && aswr.correct),
                   wrong: (question.answered && !aswr.correct && aswr.selected),
                   selected: (!question.answered && aswr.selected),
                 }"
                 @click="select(aswr)">
              <div class="game-mc__box__question__answers__item__ball">
                {{ index + 1 }}
              </div>
              <span>{{ aswr.text }}</span>
            </div>
          </div>
          <div class="game-mc__box__question__options" v-if="question.answered">
            <button v-if="!ended">Next</button>
            <button v-else>Finish</button>
          </div>
          <div class="game-mc__box__question__options" v-else>
            <button @click="confirm(question)">Confirm</button>
          </div>
        </div>
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
        question: 'Which animal does not appear in the image?',
        answers: [
          {
            text: 'Tiger',
            correct: false,
            selected: false
          },
          {
            text: 'Lion',
            correct: true,
            selected: false
          },
          {
            text: 'Bird',
            correct: false,
            selected: false
          },
          {
            text: 'Cow',
            correct: true,
            selected: false
          }
        ],
        answered: false
      },
      ended: false,
    }
  },
  methods: {
    select (answer) {
      if (!this.question.answered) {
        this.$set(answer, 'selected', true)
      }
    },
    confirm (question) {
      let questionScore = 0
      let correctCount = 0
      for (const aswr of question.answers) {
        if (aswr.correct) {
          correctCount++
          if (aswr.selected) questionScore++
        } else {
          if (aswr.selected) questionScore--
        }
      }
      if (questionScore < 0) questionScore = 0
      let score = (questionScore * 100) / correctCount
      this.$set(question, 'hit', ((questionScore * 100)/question.answers.length) >= 70 )
      this.$set(question, 'answered', true)
      console.log(question)
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
    flex-basis: calc(100% - 10px);
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
      display: flex;
      flex-direction: column;
      padding-left: 20px;
      &__text {
        text-align: left;
        flex-basis: calc(20% - 20px);
        padding: 10px 25px;
        display: flex;
        span {
          align-self: center;
          vertical-align: middle;
          font-weight: 600;
        }
      }
      &__answers {
        flex-basis: 70%;
        padding: 0px 15px;
        &__item {
          cursor: pointer;
          color: #eee;
          background-color: #999;
          margin-top: 10px;
          padding: 5px;
          height: 24px;
          border-radius: 25px;
          display: flex;
          &.right {
            background-color: green;
          }
          &.wrong {
            background-color: red;
          }
          &.selected {
            background-color: blue;
          }
          &__ball {
            background-color: #555;
            width: 15px;
            height: 15px;
            padding: 3px;
            border-radius: 25px;
            margin-right: 10px;
          }
          span {
            align-self: center;
            margin: auto 0;
          }
        }
      }
      &__options {
        flex-basis: calc(10% - 10px);
        padding: 5px 10px;
        text-align: right;
        button {
          cursor: pointer;
          padding: 10px 25px;
          font-size: 16px;
          border-radius: 25px;
          border: 2px solid transparent;
        }
      }
    }
  }
}
</style>
