<template>
  <div class="con">
    <span
        v-for="(label, index) in ['Service', 'Asset Management', 'Acquisitions & Financing', 'Property Management', 'Leasing', 'Legal']"
        :key="index"
        :class="{ active: index === activeIndex }"
        @click="setActive(index)"
    >
      {{ label }}
    </span>
  </div>
</template>

<script>
export default {
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
.con {
  display: flex;
  gap: 16px;
}

span {
  font-size: 14px;
  color: gray;
  cursor: pointer;
  text-decoration: none;
  padding: 4px 0;
  transition: color 0.3s ease;
}

span:hover {
  color: black;
}

span.active {
  color: black;
}

span::after {
  content: '';
  display: block;
  width: 0;
  height: 2px;
  background-color: #007bff;
  margin-top: 4px;
  transition: width 0.3s ease;
}

span:hover::after {
  width: 100%;
}

span.active::after {
  width: 100%;
}

</style>
