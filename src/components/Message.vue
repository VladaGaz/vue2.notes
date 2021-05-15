<template>
  <div class="message">
    {{ message }}
  </div>
</template>

<script>
export default {
  props: {
    message: {
      type: String,
      required: true,
    },
  },
};
</script>

<style  scoped>
.message {
  text-align: center;
  padding: 20px;
}
</style>