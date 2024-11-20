<template>
  <div class="container">
    <div class="partOne">
      <div style="margin-bottom: 150px;margin-left: 100px;margin-right: 100px">
        <Section v-show="prevData!==-1" class="sec bottom" :idx="active" :data="prevData" />
        <Section class="sec top" :idx="active" :data="currentData" />
      </div>
      <div class="nav">
        <Nav :active="active" @update:active="updateActive" />
        <div style="display: flex; gap: 8px; justify-content: center;">
          <img
              :src="arrowLeft"
              width="24px"
              height="24px"
              :style="{ visibility: active !== 0 ? 'visible' : 'hidden' }"
              @click="prevItem"
          />
          <img
              :src="arrowRight"
              width="24px"
              height="24px"
              :style="{ visibility: active !== images.length - 1 ? 'visible' : 'hidden' }"
              @click="nextItem"
          />
        </div>

      </div>
    </div>
    <div class="partTwo">
      <div class="image-wrapper">
        <img :src="images[prevImg]" class="prev-image" />
      </div>
      <div class="image-wrapper">
        <img :src="images[active]" class="active-image" />
      </div>
    </div>
  </div>
</template>

<script>
import gsap from "gsap"; // Import GSAP
import Nav from "@/components/Nav.vue";
import Section from "@/components/sections/body.vue";
import { data } from "@/components/sections/data.ts";
import arrowRight from "@/assets/icons/right.svg";
import arrowLeft from "@/assets/icons/left.svg";
import img1 from "@/assets/images/1.jpg";
import img2 from "@/assets/images/2.png";
import img3 from "@/assets/images/3.png";
import img4 from "@/assets/images/4.png";
import img5 from "@/assets/images/5.png";
import img6 from "@/assets/images/6.png";

export default {
  components: {
    Nav,
    Section,
  },
  data() {
    return {
      active: 0,
      prevImg: -1,
      arrowRight,
      arrowLeft,
      images: [img1, img2, img3, img4, img5, img6],
    };
  },
  computed: {
    currentData() {
      return data[this.active];
    },
    prevData(){
      return this.prevImg===-1? -1:data[this.prevImg];
    }
  },
  methods: {
    updateActive(newActive) {
      this.prevImg = this.active;
      this.active = newActive;
      this.animateImageChange();
    },
    prevItem() {
      this.prevImg = this.active;
      this.active = this.active > 0 ? this.active - 1 : this.images.length - 1;
      this.animateImageChange();
    },
    nextItem() {
      this.prevImg = this.active;
      this.active = this.active < this.images.length - 1 ? this.active + 1 : 0;
      this.animateImageChange();
    },
    animateImageChange() {
      const prevImage = document.querySelector(".prev-image");
      const activeImage = document.querySelector(".active-image");

      if (prevImage) gsap.killTweensOf(prevImage);
      if (activeImage) gsap.killTweensOf(activeImage);

      if (prevImage) {
        gsap.fromTo(
            prevImage,
            {opacity: 1, y: 0},
            {opacity: 0, y: -500, duration: 1, ease: "expo.inOut"}
        );
      }

      gsap.fromTo(
          activeImage,
          {opacity: 0, y: 1200},
          {opacity: 1, y: 0, duration: 1, ease: "expo.inOut"}
      );

      this.animateBodyChange();
    },
    animateBodyChange() {
      const prevSection = document.querySelector(".sec.bottom");
      const currentSection = document.querySelector(".sec.top");

      if (prevSection) gsap.killTweensOf(prevSection);
      if (currentSection) gsap.killTweensOf(currentSection);

      const timeline = gsap.timeline();

      if (prevSection) {
        timeline.fromTo(
            prevSection,
            {opacity: 1, y: -200},
            {opacity: 0, y: -500, duration: 1, ease: "expo.inOut"}
        );
      }

      if (currentSection) {
        timeline.fromTo(
            currentSection,
            {opacity: 0, y: 300},
            {opacity: 1, y: 0, duration: 1, ease: "expo.inOut"}
        );
      }
    },
  }
};
</script>
<style scoped lang="scss">
.container {
  position: relative;
  display: flex;
  width: 100vw;
  height: 100vh;
  overflow: hidden;
}

.partOne {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 50vw;
  height: 100vh;
  position: relative;
}

.partTwo {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 50vw;
  height: 100vh;
}
.sec{
  position: absolute;
  left: 15%;
  width: 100vw;
  &.top{
    top: 30%;
  }
  &.bottom{
    top: 55%;
  }
}
.image-wrapper {
  position: absolute;
  width: 100%;
  height: 100%;
}

.image-wrapper img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  position: absolute;
}

.nav {
  position: absolute;
  bottom: 50px;
  display: flex;
  flex-direction: column;
  gap: 32px;
}
</style>
