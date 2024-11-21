<template>
  <button class="learn-more">
    <span class="circle" aria-hidden="true">
      <span class="icon arrow"></span>
    </span>
    <span class="button-text">{{txt}}</span>
  </button>
</template>

<script>
export default {
  props: {
    txt: {
      type: String,
      default: 'Learn More'
    }
  },
}
</script>

<style scoped lang="scss">
@import url('https://fonts.googleapis.com/css?family=Mukta:700');

$bg: #f3f8fa;
$white: #fff;
$black: transparent;

@mixin transition($property: all, $duration: 0.45s, $ease: cubic-bezier(0.65,0,.076,1)) {
  transition: $property $duration $ease;
}

* {
  box-sizing: border-box;
  &::before, &::after {
    box-sizing: border-box;
  }
}

button {
  position: relative;
  display: inline-block;
  cursor: pointer;
  outline: none;
  border: 0;
  vertical-align: middle;
  text-decoration: none;
  background: transparent;
  padding: 0;
  font-size: inherit;
  font-family: inherit;
  height: 300px; /* Increased height by 1.5 times */
  &.learn-more {
    width: 37.5rem; /* Increased width by 1.5 times */
    height: 75px; /* Increased height by 1.5 times */
    .circle {
      @include transition(all, 0.45s, cubic-bezier(0.65,0,.076,1));
      position: relative;
      display: block;
      margin: 0;
      width: 4.5rem; /* Increased circle width by 1.5 times */
      height: 4.5rem; /* Increased circle height by 1.5 times */
      background: $black;
      border-radius: 2.4375rem; /* Increased border radius by 1.5 times */
      border: 2px solid white;
      .icon {
        @include transition(all, 0.45s, cubic-bezier(0.65,0,.076,1));
        position: absolute;
        top: 0;
        bottom: 0;
        margin: auto;
        background: white;
        &.arrow {
          @include transition(all, 0.45s, cubic-bezier(0.65,0,.076,1));
          left: 0.9375rem; /* Adjusted position for the increased circle */
          width: 1.6875rem; /* Increased arrow width by 1.5 times */
          height: 0.1875rem; /* Increased arrow height by 1.5 times */
          background: none;
          &::before {
            position: absolute;
            content: '';
            top: -0.375rem; /* Adjusted position for the increased arrow */
            right: 0.09375rem; /* Adjusted position for the increased arrow */
            width: 0.9375rem; /* Increased arrow before width by 1.5 times */
            height: 0.9375rem; /* Increased arrow before height by 1.5 times */
            border-top: 0.1875rem solid white; /* Increased border thickness */
            border-right: 0.1875rem solid white; /* Increased border thickness */
            transform: rotate(45deg);
          }
        }
      }
    }
    .button-text {
      @include transition(all, 0.45s, cubic-bezier(0.65,0,.076,1));
      position: absolute;
      top: 0;
      left: 15%; /* Adjusted position for the increased width */
      right: 0;
      bottom: 0;
      padding: 1.3rem .125rem 0; /* Increased padding */
      color: white;
      font-weight: 700;
      line-height: 1.6;
      text-align: left;
      text-transform: uppercase;
      font-size: 21px;
    }
  }
  &:hover {
    .circle {
      width: 100%;
      .icon {
        &.arrow {
          background: white;
          transform: translate(1.5rem, 0); /* Adjusted movement for the increased size */
        }
      }
    }
  }
}

</style>
