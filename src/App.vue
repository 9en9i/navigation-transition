<template>
  <section class="navigation" ref="navigation">
    <div class="navigation__circle" :class="{'navigation__circle_animation': useTransition}"/>
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
import {
  ref, onUnmounted,
} from 'vue';

const clickedElement = ref(0);

const navigation = ref();

const leftPadding = ref('5px');

const onClick = (index) => {
  clickedElement.value = index - 1;
  if (clickedElement.value < 4) {
    leftPadding.value = `${5 + clickedElement.value * 80}px`;
  }
  leftPadding.value = `${navigation.value.clientWidth - 75}px`;
};
const useTransition = ref(true);

const resizeHandler = (e) => {
  console.log(e);
  if (clickedElement.value === 4) {
    leftPadding.value = `${navigation.value.clientWidth - 75}px`;
  }
};

window.addEventListener('resize', resizeHandler);

onUnmounted(() => {
  window.removeEventListener('resize', resizeHandler);
});
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
    background: #5374b2;
    z-index: 10;
    border-radius: 100%;
    border: 5px solid white;
    left: v-bind(leftPadding);

    &_animation {
      transition: 2s all;
    }
  }
}
</style>
