<template>
  <div>
    <!-- Desktop -->
    <div v-show="!isMobile" class="container">
      <div class="partOne">
        <div style="margin-bottom: 150px;margin-left: 100px;margin-right: 100px">
          <div style="position: absolute;left: 0;top: 0; height: 110px;width: 25px;background-color: #2c3e50"/>
          <Section v-show="prevData !== -1" class="sec bottom" :idx="active" :data="prevData"/>
          <Section class="sec top" :idx="active" :data="currentData"/>
        </div>
        <div class="nav">
          <Nav :active="active" @update:active="updateActive"/>
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
          <img :src="images[prevImg]" class="prev-image"/>
        </div>
        <div class="image-wrapper">
          <img :src="images[active]" class="active-image"/>
          <div style="position:absolute;left: 15%; top:22%">
            <VerticalNav v-show="this.active===0" :active="active" @update:active="updateActive"/>
          </div>
        </div>
      </div>
    </div>

    <!-- Mobile -->
    <div v-show="isMobile" class="mobile-container">
      <div class="partTwoMobile">
        <div class="image-wrapper">
          <img :src="images[prevImg]" class="prev-image"/>
        </div>
        <div class="image-wrapper">
          <img :src="images[active]" class="active-image"/>
        </div>
      </div>
      <div class="partOneMobile" style="transform: scale(0.6)">
        <div style="margin-bottom: 150px;margin-left: 100px;margin-right: 100px">
          <Section v-show="prevData !== -1" class="sec bottom" :idx="active" :data="prevData"/>
          <Section class="sec top" :idx="active" :data="currentData"/>
        </div>
        <div class="nav">
          <Nav :active="active" @update:active="updateActive"/>
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
    </div>
  </div>
</template>

<script>
import gsap from "gsap";
import Nav from "@/components/Nav.vue";
import Section from "@/components/sections/body.vue";
import Btn from '@/components/Btn.vue'
import VerticalNav from "@/components/VerticalNav.vue";
import {data} from "@/components/sections/data.ts";
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
    Btn,
    VerticalNav
  },
  data() {
    return {
      active: 0,
      prevImg: -1,
      arrowRight,
      arrowLeft,
      images: [img1, img2, img3, img4, img5, img6],
      isMobile: false,
    };
  },
  computed: {
    currentData() {
      return data[this.active];
    },
    prevData() {
      return this.prevImg === -1 ? -1 : data[this.prevImg];
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
    autoChangeActive() {
      this.prevImg = this.active;
      this.active = this.active < this.images.length - 1 ? this.active + 1 : 0;
      this.animateImageChange();
    },
    checkIfMobile() {
      this.isMobile = window.matchMedia("(max-width: 768px)").matches;
    },
    // animateImageChange() {
    //   const prevImages = document.querySelectorAll(".prev-image");
    //   const activeImages = document.querySelectorAll(".active-image");
    //
    //   // Kill any existing tweens for all elements
    //   prevImages.forEach((image) => gsap.killTweensOf(image));
    //   activeImages.forEach((image) => gsap.killTweensOf(image));
    //
    //   const timeline = gsap.timeline();
    //
    //   // Animate all previous images
    //   prevImages.forEach((image, index) => {
    //     timeline.fromTo(
    //         image,
    //         { opacity: 1, y: 0 },
    //         { opacity: 1, y: -500, duration: 1, ease: "expo.inOut" },
    //     );
    //   });
    //
    //   // Animate all active images
    //   activeImages.forEach((image, index) => {
    //     timeline.fromTo(
    //         image,
    //         { opacity: 1, y: this.isMobile?100:1200 ,zIndex: 5},
    //         { opacity: 1, y: 0,zIndex: 5, duration: 2, ease: "expo.inOut" },
    //         `-=${2.5}`
    //     );
    //   });
    //
    //   // Call body change animation
    //   this.animateBodyChange();
    // },
    animateImageChange() {
      const prevImage = document.querySelector(".prev-image");
      const activeImage = document.querySelector(".active-image");

      if (prevImage) gsap.killTweensOf(prevImage);
      if (activeImage) gsap.killTweensOf(activeImage);

      if (prevImage) {
        gsap.fromTo(
            prevImage,
            {opacity: 1, y: 0},
            {opacity: 1, y: -500, duration: 1, ease: "expo.inOut"}
        );
      }

      gsap.fromTo(
          activeImage,
          {opacity: 1, y: 1200},
          {opacity: 1, y: 0, duration: 1, ease: "expo.inOut"}
      );

      this.animateBodyChange();
    },

    animateBodyChange() {
      const prevSections = document.querySelectorAll(".sec.bottom");
      const currentSections = document.querySelectorAll(".sec.top");

      prevSections.forEach((section) => gsap.killTweensOf(section));
      currentSections.forEach((section) => gsap.killTweensOf(section));

      const timeline = gsap.timeline();

      prevSections.forEach((section, index) => {
        timeline.fromTo(
            section,
            {opacity: 1, y: -250},
            {opacity: 0, y: this.isMobile ? -300 : -500, duration: this.isMobile ? 1.6 : 2, ease: "power3.out"},
            index * 0.2
        );
      });

      currentSections.forEach((section, index) => {
        timeline.fromTo(
            section,
            {opacity: 0, y: 200},
            {opacity: 1, y: 0, duration: this.isMobile ? 2.8 : 2, ease: "power3.out"},
            `-=${1.5 - index * -0.8}`
        );
      });
    },
  },
  mounted() {
    this.checkIfMobile();
    window.addEventListener("resize", this.checkIfMobile);
    setInterval(this.autoChangeActive, 5000);
  },
  beforeDestroy() {
    window.removeEventListener("resize", this.checkIfMobile);
  },
};
</script>

<style scoped lang="scss">
.mobile-container {
  position: relative;
  display: flex;
  flex-direction: column;
  width: 100vw;
  height: 100vh;
  overflow: hidden;
}

.container {
  position: relative;
  display: flex;
  width: 100vw;
  height: 100vh;
  overflow: hidden;
}

.partOneMobile {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 100vw;
  height: 70vh;
  position: relative;
  z-index: 10;
}

.partTwoMobile {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100vw;
  height: 30vh;
  z-index: 5;
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

.sec {
  position: absolute;
  left: 15%;
  width: 100vw;

  &.top {
    top: 25%;
    @media (max-width: 768px) {
      top: 0;
    }
  }

  &.bottom {
    top: 55%;
    @media (max-width: 768px) {
      top: 20%;
    }
  }

  @media (max-width: 768px) {
    left: -100px;
  }
}

.image-wrapper {
  position: absolute;
  width: 100%;
  height: 100%;
  z-index: -10;
}

.image-wrapper img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  position: absolute;
  z-index: -10;
}

.nav {
  position: absolute;
  bottom: 50px;
  display: flex;
  flex-direction: column;
  gap: 32px;
  @media (max-width: 768px) {
    bottom: -100px;
  }
}
</style>
