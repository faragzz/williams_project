<template>
  <div class="container">
    <div class="partOne">
      <div style="margin-bottom: 150px;position: relative;margin-left: 100px;margin-right: 100px">
        <Section :idx="active" :data="prevData" />
        <Section :idx="active" :data="currentData" />
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
      prevImg: 1, // To track the previous image
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
      return data[this.prevImg];
    }
  },
  methods: {
    updateActive(newActive) {
      this.prevImg = this.active; // Update previous image index
      this.active = newActive; // Update active image index
      this.animateImageChange();
    },
    prevItem() {
      this.prevImg = this.active; // Update previous image index
      this.active = this.active > 0 ? this.active - 1 : this.images.length - 1;
      this.animateImageChange();
    },
    nextItem() {
      this.prevImg = this.active; // Update previous image index
      this.active = this.active < this.images.length - 1 ? this.active + 1 : 0;
      this.animateImageChange();
    },
    animateImageChange() {
      const prevImage = document.querySelector(".prev-image");
      const activeImage = document.querySelector(".active-image");

      // Animate the previous image out
      if (prevImage) {
        gsap.fromTo(prevImage,
            { opacity: 1, y: 0 },
            { opacity: 1, y: -500, duration: 2.2, ease: "expo.inOut" }
        );
      }

      // Animate the new image in
      gsap.fromTo(
          activeImage,
          { opacity: 1, y: 1200 }, // Start below and invisible
          { opacity: 1, y: 0, duration: 2, ease: "expo.inOut" }
      );
    },
  },
};
</script>
<style scoped>
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
  left: -500px;
  top: 50%;
  width: 100vw;
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
