<template>
  <div class="page">
    <div class="page-content">
      <h1 @click="easterEgg">HISTORY</h1>
      <h2>
        <span class="fun">{{ funText.slice(0, funIndex) }}</span>
        역사 공부를 합시다.
      </h2>
      <h3>원하는 모드를 선택해주세요.</h3>
      <nav class="button-wrap">
        <button
          @click="$router.push({ name: 'questionWord', params: { mode: 1 } })"
        >
          <span>2학년 2학기</span>
          <span class="bold">중간고사</span>
        </button>
      </nav>
      <router-link
        to="/word"
        style="color: black; margin-top: 30px; font-size: 1.25rem"
      >
        정답 보러 가기
      </router-link>
    </div>

    <Footer />
  </div>
</template>

<script>
import Footer from "@/components/Footer";

export default {
  name: "MainPage",
  data() {
    return {
      funText: "세상에서 제일 재밌는",
      funIndex: -1, //this.funText.length,
      easterEggCount: 0,
    };
  },
  components: {
    Footer,
  },
  methods: {
    easterEgg() {
      this.easterEggCount++;

      if (this.easterEggCount == 50) {
        alert("이렇게나 역사에 대한 흥미가 높다니... 100점 맞으시겠네요 👏👏");
      } else if (this.easterEggCount == 100) {
        alert("너무 클릭하셔서 HISTORY라는 문자가 사라지겠어요...");
      }
    },
  },
  mounted() {
    this.funIndex = this.funText.length;
    setTimeout(() => {
      setInterval(() => {
        if (this.funIndex === 0) return;

        this.funIndex--;
      }, 150);
    }, 700);
  },
};
</script>

<style>
.page {
  padding-top: 0px;
}

.page-content {
  width: 63%;
  height: 63%;

  display: flex;
  flex-direction: column;
  align-items: center;
}

h1 {
  font-weight: 900;
  font-size: 5rem;
  line-height: 154px;

  text-align: center;

  background: linear-gradient(
    94deg,
    rgba(200, 200, 200, 1) 0%,
    rgba(19, 19, 19, 1) 100%
  );
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;

  margin: 0px auto 0;

  display: inline-block;
}

h2 {
  font-weight: 800;
  font-size: 2.25rem;

  text-align: center;
}

.fun {
  text-decoration: 10px;
  font-weight: 500;
  color: var(--gray5);
}

h3 {
  font-size: 1.75rem;
  font-weight: normal;
  text-align: center;
  color: #838383;

  /*animation-name : comment-animation;*/
  /*animation-duration: 2000ms;*/
  /*animation-iteration-count: infinite;*/
}

.button-wrap {
  width: 80%;
  margin-top: 20px;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(210px, auto));
  gap: 40px;
}

.button-wrap > button {
  font-size: 28px;
  font-weight: 500;

  color: white;

  padding: 20px 44px;
  border-radius: 20px;

  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;

  cursor: pointer;
}

.button-wrap > button:hover {
  background-color: white;
  color: black;
  border: 2px solid black;
}

.button-wrap > button:active {
  opacity: 0.7;
  transform: scale(0.985);
}

@keyframes comment-animation {
  0%,
  100% {
    /*transform: scale(1);*/
    transform: translateY(0);
  }
  50% {
    /*transform: scale(1.05);*/
    transform: translateY(20px);
  }
}

/* 모바일 디자인 (태블릿 가로) */
@media (max-width: 900px) {
  .page-content {
    width: 80%;
    height: 60%;
  }
}

/* 핸드폰 세로 */
@media (max-width: 400px) {
  .page-content {
    width: 100%;
    padding-top: 0px;
  }

  h1 {
    font-size: 4rem;
  }

  h2 {
    font-size: 2rem;
    margin-top: 0px;
  }

  .copyright {
    font-size: 1.05rem;
  }

  footer {
    margin-top: 0px;
  }
}
</style>
