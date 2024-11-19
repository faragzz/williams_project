<script>

export default {
  name: "Body",
  props: {
    data: {
      type: Object,
      required: true
    },
    idx: {
      type: Number,
      required: true
    }
  },
  computed: {
    showWhatToDo() {
      return this.idx > 0;
    }
  }
};
</script>

<template>
  <div >
    <p class="what-to-do" v-show="showWhatToDo">WHAT WE DO</p>
    <p class="title">{{ data.title }}</p>
    <p class="paragraph">{{ data.paragraph }}</p>
  </div>
</template>

<style scoped>
.what-to-do {
  font-size: 18px;
  color: #2596be;
}

.title {
  font-size: 38px;
  width: 200px;
  margin-top: -10px;
}

.paragraph {
  font-size: 18px;
}
</style>
