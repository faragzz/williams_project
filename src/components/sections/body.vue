<template>
  <div :style="{ width: isMobile ? '160%' : '700px' }" ref="content">
    <p class="what-to-do" v-show="showWhatToDo">WHAT WE DO</p>
    <p class="title">{{ data.title }}</p>
    <p class="paragraph">{{ data.paragraph }}</p>
  </div>
</template>

<script>
import {gsap} from "gsap";

export default {
  name: "Body",
  data(){
    return {
      isMobile: false,
    }
  },
  props: {
    data: {type: Object, required: true},
    idx: {type: Number, required: true},
  },
  computed: {
    showWhatToDo() {
      return this.idx > 0;
    },
  },
  watch: {
    idx() {
      this.animateText(); // Trigger animation when idx changes
    },
  },
  methods: {
    animateText() {
      const content = this.$refs.content;
      if (!content) {
        console.warn("No content found for animation.");
        return;
      }

      const elements = content.querySelectorAll("p");
      if (!elements.length) {
        console.warn("No <p> elements found for animation.");
        return;
      }

      const timeline = gsap.timeline();
      elements.forEach((el, index) => {
        timeline.fromTo(
            el,
            {opacity: 0, y: 50},
            {opacity: 1, y: 0, duration: 0.6, ease: "power2.out"},
            index * 0.3 // Stagger animations
        );
      });
    },
    checkIfMobile() {
      this.isMobile = window.matchMedia("(max-width: 768px)").matches;
    },
  },
  mounted() {
    this.animateText(); // Run animation on initial render
    this.checkIfMobile();
    window.addEventListener("resize", this.checkIfMobile);
  },
  beforeDestroy() {
    window.removeEventListener("resize", this.checkIfMobile);
  },
};
</script>

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
