<template>
  <div class="container">
    <button class="learn-more" @click="onClick">
      <span class="circle" aria-hidden="true">
        <span class="icon arrow"></span>
        <span class="button-text">{{ buttonText }}</span>
      </span>
    </button>
  </div>
</template>

<script>
export default {
  name: 'LearnMoreButton',
  props: {
    buttonText: {
      type: String,
      default: 'Learn More'
    }
  },
  methods: {
    onClick() {
      // Logic for the button click can go here
      console.log('Button clicked!');
    }
  }
}
</script>

<style scoped lang="scss">
@import url('https://fonts.googleapis.com/css?family=Mukta:700');

$bg: black;
$white: black;
$black: transparent;

@mixin transition($property: all, $duration: 0.45s, $ease: cubic-bezier(0.65,0,.076,1)) {
  transition: $property $duration $ease;
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

  &.learn-more {
    max-width: 200px; /* Max width to prevent the button from being too large */
    width: 100%; /* Responsive width */
    .circle {
      @include transition(all, 0.45s, cubic-bezier(0.65,0,.076,1));
      position: relative;
      display: block;
      margin: 0;
      width: 3rem;
      height: 3rem;
      background: $black;
      border-radius: 1.625rem;
      border: 2px solid black;
      .icon {
        @include transition(all, 0.45s, cubic-bezier(0.65,0,.076,1));
        position: absolute;
        top: 0;
        bottom: 0;
        margin: auto;
        background: black;

        &.arrow {
          @include transition(all, 0.45s, cubic-bezier(0.65,0,.076,1));
          left: 0.625rem;
          width: 1.125rem;
          height: 0.125rem;
          background: none;
          &::before {
            position: absolute;
            content: '';
            top: -0.25rem;
            right: 0.0625rem;
            width: 0.625rem;
            height: 0.625rem;
            border-top: 0.125rem solid black;
            border-right: 0.125rem solid black;
            transform: rotate(45deg);
          }
        }
      }
    }
    .button-text {
      @include transition(all, 0.45s, cubic-bezier(0.65,0,.076,1));
      position: absolute;
      top: 0;
      left: 50px;
      right: 0;
      bottom: 0;
      padding: 0.75rem 0;
      margin: 0 0 0 1.85rem;
      color: $black;
      font-weight: 700;
      line-height: 1.6;
      text-align: center;
      text-transform: uppercase;
    }
  }

  &:hover {
    .circle {
      width: 100%;
      .icon {
        &.arrow {
          background: $white;
          transform: translate(1rem, 0);
        }
      }
    }
    .button-text {
      color: $white;
    }
  }
}


.container {
  align-self: center;
  justify-self: center;
  display: flex;
  justify-content: center; /* Center button horizontally */
}
</style>
