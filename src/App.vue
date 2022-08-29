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
      <span
        >&lt;a class="report" <span>href</span>="{{
          userInput.split(/\r?\n/)[0]
        }}"&gt;</span
      >
      <fakeTag tag="h2">{{ userInput.split(/\r?\n/)[1] }}</fakeTag>
      <div v-if="userInput.split(/\r?\n/)[1]">
        <fakeTag v-for="n in userInput.split(/\r?\n/).length - 2" tag="p">{{
          userInput.split(/\r?\n/)[n + 1]
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
      userInput: "",
      projects: [
        {
          name: "🌕 Serenity Основной сайт",
          link: "https://www.notion.so/odva/446ab218c4c44d44bbe2dde8fe472c70?v=f5ec53126359412dbe1bbcaa3e5efe08",
        },
        {
          name: "🥗 Вкусно и быстро",
          link: "https://www.notion.so/odva/446ab218c4c44d44bbe2dde8fe472c70?v=f5ec53126359412dbe1bbcaa3e5efe08",
        },
        {
          name: "7️⃣ Seven+",
          link: "https://www.notion.so/odva/446ab218c4c44d44bbe2dde8fe472c70?v=f5ec53126359412dbe1bbcaa3e5efe08",
        },
        {
          name: "🎮 YourGame (COINT)",
          link: "https://www.notion.so/odva/446ab218c4c44d44bbe2dde8fe472c70?v=f5ec53126359412dbe1bbcaa3e5efe08",
        },
        {
          name: "💉 РУДН Клиника",
          link: "https://www.notion.so/odva/446ab218c4c44d44bbe2dde8fe472c70?v=f5ec53126359412dbe1bbcaa3e5efe08",
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
  text-align: center;
  margin-bottom: 2rem;
}
select {
  text-align: center;
  font-family: inherit;
  font-size: 1.5rem;
}
.mainlink {
  cursor: pointer;
  background-color: #ddd;
  color: #111;
  display: block;
  text-align: center;
  padding: 1rem 3rem;
}
.app {
  display: grid;
  grid-template-columns: 1fr 1fr;
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
  flex-basis: 50%;
  padding: 3rem;
}
.code {
  font-size: 0.75rem;
  background-color: #222;
}
</style>
