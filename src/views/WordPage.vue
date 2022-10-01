<template>
  <div class="page">
    <div class="page-content">
      <div class="title">
        <div class="question">
          {{ wordData.question }}
        </div>
        <div class="answer">
          {{ wordData.answer }}
        </div>
        <div class="textbook-page">교과서 {{ wordData.page }}쪽</div>
      </div>

      <div class="button-wrap">
        <div class="prev-next-wrap">
          <button
            @click="prevClick"
            class="prev only-border"
            :class="{ 'enabled-none': idx === 0, 'none-dragging': idx == 0 }"
          >
            이전
          </button>
          <button
            @click="nextClick"
            class="next"
            :class="{ 'enabled-none': idx === 83 }"
          >
            다음
          </button>
        </div>
        <router-link
          to="/"
          style="
            color: black;
            margin-top: 30px;
            font-size: 1.25rem;
            text-align: center;
          "
        >
          홈으로 가기
        </router-link>
      </div>
    </div>
    <Footer />
  </div>
</template>

<script>
import wordData from "./../data/wordData.js";
import Footer from "@/components/Footer";

export default {
  name: "QuestionPage",
  data() {
    return {
      idx: 0,
      wordDataList: wordData.sort(function (a, b) {
        if (a.id > b.id) {
          return 1;
        } else if (a.id < b.id) {
          return -1;
        }
        return 0;
      }),
      wordData: {},
    };
  },
  components: {
    Footer,
  },
  methods: {
    setWord() {
      this.wordData = this.wordDataList[this.idx];
    },
    prevClick() {
      if (this.idx !== 0) this.idx--;
    },
    nextClick() {
      if (this.idx < 84) this.idx++;
    },
  },
  watch: {
    idx() {
      this.setWord();
    },
  },
  mounted() {
    this.setWord();
  },
};
</script>

<style scoped>
.page-content {
  padding: 60px 0;

  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 75px;
}

.title {
  text-align: center;
}

.question {
  font-size: 30px;
  font-weight: bold;
}

.answer {
  color: var(--gray6);
  margin-top: 30px;
  font-size: 40px;
  font-weight: bold;
  text-align: center;
}

.textbook-page {
  font-size: 25px;
  font-weight: bold;
  text-align: center;
  margin-top: 20px;
}

.button-wrap {
  width: 100%;

  margin-top: 50px;

  display: flex;
  flex-direction: column;
  gap: 95px;
}

.prev-next-wrap {
  width: 100%;

  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 20px;
}

button {
  font-size: 28px;
  font-weight: 600;
}

@media (max-width: 900px) {
  .question {
    font-size: 1.5rem;
  }
}
</style>
