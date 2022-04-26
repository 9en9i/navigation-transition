<template>
  <section class="navigation">
    <div class="navigation__circle" :class="{'navigation__circle_right': clickedElement === 4 }"/>
    <div class="navigation__button-wrap">
      <button v-for="index in 4" class="navigation__button" @click="onClick(index)" :key="index">
        {{index}}
      </button>
    </div>
    <button class="navigation__button" @click="onClick(5)">
      5
    </button>
  </section>
</template>

<script setup>
import { ref } from 'vue';

const clickedElement = ref(0);
const onClick = (index) => {
  clickedElement.value = index - 1;
};
</script>

<style lang="scss" scoped>
.navigation {
  margin: 50px 30px;
  background: #42b983;
  display: flex;
  justify-content: space-between;
  position: relative;

  &__button-wrap {
    display: flex;
  }

  &__button {
    border: unset;
    background-color: unset;
    margin: 0 20px 20px 20px;
    width: 40px;
    height: 40px;
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 20;
    cursor: pointer;
  }

  &__circle {
    width: 60px;
    height: 60px;
    position: absolute;
    top: -20px;
    left: calc(5px + v-bind(clickedElement) * 80px);
    background: #5374b2;
    z-index: 10;
    border-radius: 100%;
    border: 5px solid white;
    transition: 2s all;

    &_right {
      left: calc(100% - 75px);
    }
  }
}
</style>
