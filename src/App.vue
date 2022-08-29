<template>
  <h1>O&#8322; Reporter</h1>

  <div class="app">
    <textarea
      class="raw"
      v-model="test"
      name=""
      id=""
      cols="30"
      rows="10"
    ></textarea>
    <div ref="output" class="code">
      <span
        >&lt;a class="report" <span>href</span>="{{
          test.split(/\r?\n/)[0]
        }}"&gt;</span
      >
      <fakeTag tag="h2">{{ test.split(/\r?\n/)[1] }}</fakeTag>
      <div v-if="test.split(/\r?\n/)[1]">
        <fakeTag v-for="n in test.split(/\r?\n/).length - 2" tag="p">{{
          test.split(/\r?\n/)[n + 1]
        }}</fakeTag>
      </div>
      <fakeTag tag="style">
        <span
          >.calendar-day[data-success="1"]{background-color:orange}.report{color:#111}.report
          h2{font-weight:bold;margin-bottom:2rem;font-size:3rem}.report
          p:last-of-type{margin-bottom:-1rem}</span
        >
      </fakeTag>
      <span>&lt;/a&gt;</span>
    </div>
  </div>
  <div @click="copyAndGo" class="mainlink">Go to Report</div>
  <div class="help">
    <h2>Как это работает</h2>
    <p>В первую строчку идет ссылка — не забудьте https://</p>
    <p>Во вторую строку идет название задачи</p>
    <p>При желании можно добавить описание (3 строчка и далее)</p>
  </div>
</template>

<script>
import fakeTag from "./components/fakeTag.vue";

export default {
  components: {
    fakeTag,
  },
  data() {
    return {
      test: "",
    };
  },
  methods: {
    copy() {
      navigator.clipboard.writeText(this.$refs.output.textContent);
    },
    copyAndGo() {
      this.copy();
      window.open("https://report.odva.pro/");
    },
  },
};
</script>

<style>
h1 {
  text-align: center;
  margin-bottom: 2rem;
}
.mainlink {
  cursor: pointer;
  background-color: #ddd;
  color: #111;
  display: block;
  text-align: center;
  padding: 1rem 3rem;
  margin-bottom: 2rem;
}
.app {
  display: flex;
  margin-bottom: 2rem;
}
.help {
  text-align: center;
  color: #999;
}
.help h2 {
  color: #ddd;
}
span span {
  color: orange;
}
.raw,
.code {
  font-size: 1rem;
  flex: 1;
  padding: 3rem;
}
.code {
  background-color: #222;
}
</style>
