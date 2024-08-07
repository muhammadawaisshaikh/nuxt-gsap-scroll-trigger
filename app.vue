<script setup>
import { onMounted, onUnmounted, ref } from 'vue';
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';

gsap.registerPlugin(ScrollTrigger);

const main = ref();
let ctx;

onMounted(() => {
  ctx = gsap.context((self) => {
    const boxes = self.selector('.box');
    boxes.forEach((box) => {
      gsap.to(box, {
        x: 150,
        scrollTrigger: {
          trigger: box,
          start: 'bottom bottom',
          end: 'top 20%',
          scrub: true,
        },
      });
    });
  }, main.value); // <- Scope!
});

onUnmounted(() => {
  ctx.revert(); // <- Easy Cleanup!
});
</script>

<template>
  <section class="panel center column gradient-blue text-dark">
    <h1>Basic ScrollTrigger in Nuxt 3</h1>
    <h2>Scroll down to see the magic happen!!</h2>
    <a href="#">Author: Muhammad Awais</a>
  </section>
  <div class="panel center column" ref="main">
    <div class="box gradient-green">box</div>
    <div class="box gradient-green">box</div>
    <div class="box gradient-green">box</div>
  </div>
  <section class="panel center gradient-orange column text-dark">
    <h1>The End!</h1>
    <h2 class="center">
      For more information visit:&nbsp;
      <a href="https://greensock.com/scrolltrigger/" target="_blank" rel="noreferrer">
        greensock.com/scrolltrigger/
      </a>
    </h2>
  </section>
</template>

<style>
@import url('~/assets/styles.css');
</style>
