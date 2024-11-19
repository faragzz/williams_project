<template>
  <div class="container">

    <div class="partOne">
      <div class="nav">
        <Nav :active="active" @update:active="updateActive"/>
        <div style="display: flex; gap: 8px; justify-content: center;">
          <img :src="arrowLeft" width="24px" height="24px" v-show="active !== 0" @click="prevItem" />
          <img :src="arrowRight" width="24px" height="24px" v-show="active !== 5" @click="nextItem"/>
        </div>
      </div>
    </div>
    <div class="partTwo">

    </div>
  </div>
</template>

<script scoped>
import Nav from './components/Nav.vue';
import arrowRight from '../src/assets/icons/right.svg'
import arrowLeft from '../src/assets/icons/left.svg'
export default {
  components: {
    Nav,
  },
  data() {
    return {
      active: 0,
      arrowRight,
      arrowLeft
    };
  },
  methods: {
    updateActive(newActive) {
      this.active = newActive;
    },
    prevItem() {
      if (this.active > 0) {
        this.active--;
      } else {
        this.active = 5; // Wrap to the last item
      }
    },
    nextItem() {
      if (this.active < 5) {
        this.active++;
      } else {
        this.active = 0; // Wrap to the first item
      }
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
}
.partOne{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background-color: lemonchiffon;
  width: 50vw;
  height: 100vh;
}
.partTwo{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background-color: cyan;
  width: 50vw;
  height: 100vh;
}
.nav {
  position: absolute;
  bottom: 50px;
  display: flex;
  flex-direction: column;
  gap:32px;
}
</style>
