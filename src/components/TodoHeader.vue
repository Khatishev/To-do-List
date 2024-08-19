<template>
  <div class="container">
    <h1>To-do List!</h1>
    <h3>Notes: {{ noteCount }}</h3>
    <div class="time"><b>{{ formattedDate }}</b></div>
  </div>
</template>

<script>
export default {
  name: 'TodoHeader',
  props: {
    noteCount: {
      type: Number,
      required: true
    },
    formattedDate: {
      type: String,
      required: true
    }
  }
};
</script>

<style scoped></style>