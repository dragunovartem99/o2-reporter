<template>
  <span>&lt;{{ type }}&gt;</span><slot /><span>&lt;/{{ type }}&gt</span>
</template>
<script>
export default {
  props: ["type"],
};
</script>
<style>
span {
  color: orange;
}
</style>
