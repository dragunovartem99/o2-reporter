<template>
  <h1>O&#8322; Reporter</h1>
  <div class="app">
    <textarea v-model="test" name="" id="" cols="30" rows="10"></textarea>
    <div class="code">
      <fakeTag type="p">{{ test }}</fakeTag>
    </div>
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
};
</script>

<style scoped>
h1 {
  text-align: center;
}
.app {
  display: flex;
}
.code {
}
</style>
