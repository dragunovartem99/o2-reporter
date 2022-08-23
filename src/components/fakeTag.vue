<template>
  <span> &lt;{{ type }}&gt;<slot />&lt;/{{ type }}&gt; </span>
</template>
<script>
export default {
  props: ["type"],
};
</script>
