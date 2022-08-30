<template>
  <h1>O&#8322; Reporter</h1>
  <div class="app">
    <textarea
      class="raw"
      ref="input"
      v-model="userInput"
      name=""
      id=""
      cols="30"
      rows="10"
    ></textarea>
    <div ref="output" class="code">
      <span>
        <span>&lt;a</span> <span class="code--bleak">class="report" href="</span
        >{{ userInput.split(/\r?\n/)[0] }}<span class="code--bleak">"</span
        ><span>&gt;</span></span
      >
      <fakeTag tag="h2">{{ userInput.split(/\r?\n/)[1] }}</fakeTag>
      <div v-if="userInput.split(/\r?\n/)[1]">
        <fakeTag v-for="n in userInput.split(/\r?\n/).length - 2" tag="p">{{
          userInput.split(/\r?\n/)[n + 1]
        }}</fakeTag>
      </div>
      <fakeTag class="code--bleak" tag="style">
        <span
          >.report{color:#111}.report
          h2{font-weight:bold;margin-bottom:2rem;font-size:3rem}.report
          p:last-of-type{margin-bottom:-1rem}</span
        >
      </fakeTag>
      <span><span>&lt;/a&gt;</span></span>
    </div>
    <select @change="setProject">
      <option>Выбери проект</option>
      <option v-for="project in projects">
        {{ project.name }}
      </option>
    </select>
    <div @click="copyAndGo" class="mainlink">Go to Report</div>
  </div>
  <div class="help">
    <h2>Как это работает</h2>
    <p>В первую строку идет ссылка — не забудьте https://</p>
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
      userInput: "",
      projects: [
        {
          name: "🌕 Serenity Основной сайт",
          link: "https://noto.li/Z8ZDpC",
        },
        {
          name: "🥗 Вкусно и быстро",
          link: "https://noto.li/RI1cjr",
        },
        {
          name: "7️⃣ Seven+",
          link: "https://noto.li/I7tzu5",
        },
        {
          name: "🎮 YourGame (COINT)",
          link: "https://noto.li/tDWQi4",
        },
        {
          name: "💉 РУДН Клиника",
          link: "https://noto.li/Lvu0fX",
        },
      ],
    };
  },
  methods: {
    setProject(event) {
      const selectedProject = this.projects.find(
        (o) => o.name === event.target.value
      );
      this.userInput =
        selectedProject.link + "\n" + selectedProject.name + "\n";
      this.$refs.input.focus();
    },

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
  margin-top: 2rem;
  text-align: center;
}

.mainlink,
select {
  font-size: 1.25rem;
}

select {
  text-align: center;
  font-family: inherit;
  background: repeating-linear-gradient(
    -45deg,
    #fff,
    #fff 2rem,
    #f7f7f7 2rem,
    #f7f7f7 4rem
  );
}
.mainlink {
  cursor: pointer;
  background-color: darkorange;
  color: #111;
  display: block;
  text-align: center;
  padding: 1rem 3rem;
}
.app {
  margin-block: auto;
  display: grid;
  grid-template-columns: 1fr 1fr;
}
.help {
  text-align: center;
  color: #aaa;
  margin-bottom: 2rem;
}
.help h2 {
  color: #eee;
}
.raw,
.code {
  padding: 3rem;
  font-size: 1rem;
}
.raw {
  font-family: inherit;
  resize: none;
}
.code {
  background-color: #1a1a1a;
}
span span {
  color: #6a6a6a;
}
.code--bleak {
  color: #aaa;
}
</style>
