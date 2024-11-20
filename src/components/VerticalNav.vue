<template>
  <div class="container">
    <span
        v-for="(label, index) in ['Service', 'Asset Management', 'Acquisitions & Financing', 'Property Management', 'Leasing', 'Legal']"
        :key="index"
        @click="setActive(index)"
    >
      <Btn :txt="label"/>
    </span>
  </div>
</template>

<script>
import Btn from './Btn.vue'

export default {
  components: {
    Btn
  },
  props: {
    active: {
      type: Number,
      default: 0,
    },
  },
  data() {
    return {
      activeIndex: this.active,
    };
  },
  watch: {
    active(newActive) {
      this.activeIndex = newActive;
    },
  },
  methods: {
    setActive(index) {
      this.activeIndex = index;
      this.$emit("update:active", index);
    },
  },
};
</script>

<style scoped>
.container{
  display: flex;
  flex-direction: column;
  gap: 1rem;
}
</style>
