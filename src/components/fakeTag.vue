<template>
  <div class="faketag">
    <span> &lt;{{ tag }}&gt;</span><slot /><span>&lt;/{{ tag }}&gt</span>
  </div>
</template>
<script>
export default {
  props: ["tag"],
};
</script>
<style scoped>
span {
  color: #999;
}
.faketag {
  margin-left: 1rem;
}
</style>
