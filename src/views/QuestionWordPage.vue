<template>
  <div class="page">
    <div class="page-content">
      <div class="title">
        <h2>
          <span
            >문제에 해당하는 <span class="bold">답을 선택해주세요.</span></span
          >
        </h2>

        <span class="question" :class="{ isAnswer: isAnswer }">{{
          questionMode == 0 ? wordList[0].question : wordList[0].ko
        }}</span>
      </div>

      <div class="options-wrap">
        <div
          v-for="(i, n) in optionList"
          :key="n"
          @click="
            () => {
              checkAnswer(i.id, n);
            }
          "
          class="option"
          :class="{ 'wrong-answer': state[n] == 1, answer: state[n] == 2 }"
        >
          {{
            questionMode == 0 ? optionList[n].answer : optionList[n].question
          }}
        </div>
      </div>
    </div>
    <Footer />
  </div>
</template>

<script>
import Footer from "@/components/Footer";
import * as util from "./../util/util.js";
import wordData from "./../data/wordData";

let wordList = util.shuffle(wordData);
let optionList = util.shuffle(wordList.slice(0, 5));

export default {
  name: "QuestionPage",
  data() {
    return {
      wordList,
      optionList,

      answerId: -1,
      state: [0, 0, 0, 0, 0],
      isAnswer: false,
      con: 0,

      questionMode: this.$route.params.mode,
    };
  },
  components: {
    Footer,
  },
  methods: {
    setQuestion() {
      this.wordList = util.shuffle(this.wordList);
      this.optionList = util.shuffle(this.wordList.slice(0, 5));
      this.answerId = wordList[0].id;
      this.isAnswer = false;
      this.state = [0, 0, 0, 0, 0];
    },
    checkAnswer(id, idx) {
      if (this.isAnswer) return;

      if (id == this.answerId) {
        this.isAnswer = true;
        this.state[idx] = 2;

        this.con += 1;

        setTimeout(() => {
          this.setQuestion();
        }, 1000);
      } else {
        this.state[idx] = 1;
        this.con = 0;
      }
    },
  },
  mounted() {
    if (this.questionMode == undefined) this.questionMode = 0;
    this.setQuestion();
  },
};
</script>

<style scoped>
.page-content {
  padding: 80px 0;

  display: flex;
  flex-direction: column;
  align-items: center;
}

.title {
  text-align: center;

  transition: 200ms;
}

.isAnswer {
  color: var(--correct);
}

h2 {
  font-size: 2rem;
  font-weight: 500;

  display: flex;
  flex-direction: column;
  align-items: center;

  margin-top: 0px;
}

.question {
  font-size: 1.5rem;
  font-weight: bold;

  width: 1000px;
}

.options-wrap {
  width: 80%;

  margin-top: 61px;

  display: flex;
  flex-direction: column;
  gap: 28px;
}

.options-wrap > .option {
  color: var(--flat-black);

  text-align: center;
  font-size: 2rem;
  font-weight: bold;

  padding: 12px 0;

  border: solid 1px var(--gray5);
  border-radius: 20px;
  background-color: #fff;

  position: relative;

  transition: 150ms;

  cursor: pointer;
  width: 80%;
  height: 50px;

  margin: 0px auto;
}

.options-wrap > .option:hover {
  color: #fff;
  background-color: var(--main-color1);
  border: 1px solid var(--main-color1);
}
.options-wrap > .option:active {
  opacity: 0.7;
  transform: scale(0.985);
}

.options-wrap > .option.wrong-answer {
  background-color: var(--flat-red);
  color: white;
  border: 1px solid var(--flat-red);
}

.options-wrap > .option.answer {
  background-color: var(--correct);
  color: white;
  border: 1px solid var(--correct);
}

@media (max-width: 900px) {
  .page-content {
    padding-top: 30px;
  }

  h2 {
    font-size: 20px;
  }

  .title {
    width: 90%;
  }

  .options-wrap {
    margin-top: 20px;
    width: 90%;
  }

  .options-wrap > .option {
    height: 40px;
  }

  .question {
    font-size: 1.2rem;
  }

  .options-wrap {
    gap: 24px;
  }

  .options-wrap > .option {
    font-size: 28px;

    padding: 8px 0px;
    border-radius: 8px;
  }

  footer {
    margin-top: 0px;
  }
}
</style>
