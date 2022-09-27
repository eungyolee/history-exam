<template>
  <footer>
    <div class="content">
      <div class="copyright">
        <span
          >Developed by
          <a href="https://eungyolee.github.io" target="_blank"
            >이은교 (Eun-Gyo Lee)</a
          ></span
        >
        <span>Copyright 2022. 이은교 all rights reserved.</span>
      </div>
      <!-- <div class="open-source">
      <a href="https://www.github.com/ckstmznf/Hiragana" target="_blank">오픈소스 라이선스</a>
    </div> -->
    </div>
  </footer>
</template>

<script>
export default {
  name: "Footer",
};
</script>

<style scoped>
footer {
  width: 100%;

  padding: 34px 16px;

  background: #fdfdfd;
  border-top: 1px solid #c2c2c2;
  box-sizing: border-box;
}
.content {
  width: 100%;
  max-width: 1000px;

  font-size: 20px;
  font-weight: 300;
  line-height: 24px;

  margin: 0 auto;

  display: flex;
  justify-content: space-between;
}

a {
  font-weight: 500;
  color: black;
}

.copyright {
  display: flex;
  flex-direction: column;
  gap: 8px;
}
.open-source {
  display: flex;
  align-items: flex-end;
}
</style>
