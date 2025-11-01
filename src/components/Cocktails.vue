<script setup>
import { ref, onMounted } from "vue";
import { cocktailLists, mockTailLists } from "../../constants";
import gsap from "gsap";
import { ScrollTrigger } from "gsap/all";

gsap.registerPlugin(ScrollTrigger);

onMounted(() => {
  const parallaxTimeline = gsap.timeline({
    scrollTrigger: {
      trigger: "#cocktails",
      start: "top 30%",
      end: "bottom 80%",
      scrub: true,
    },
  });

  parallaxTimeline.from("#c-left-leaf", {
    x: -100,
    y: 100,
  });
  parallaxTimeline.from("#c-right-leaf", {
    x: 100,
    y: 100,
  });
});
</script>

<template>
  <section id="cocktails" class="noisy">
    <img
      src="/images/cocktail-left-leaf.png"
      alt="left-leaf"
      id="c-left-leaf"
    />
    <img
      src="/images/cocktail-right-leaf.png"
      alt="right-leaf"
      id="c-right-leaf"
    />
    <div class="list">
      <div class="popular">
        <h2>Most popular cocktails:</h2>
        <ul>
          <li v-for="cocktail in cocktailLists" :key="cocktail.name">
            <div class="md:me-28">
              <h3>{{ cocktail.name }}</h3>
              <p>{{ cocktail.country }} | {{ cocktail.detail }}</p>
            </div>
            <span>{{ cocktail.price }}</span>
          </li>
        </ul>
      </div>
      <div class="loved">
        <h2>Most loved mocktails:</h2>
        <ul>
          <li v-for="mocktail in mockTailLists" :key="mocktail.name">
            <div class="me-28">
              <h3>{{ mocktail.name }}</h3>
              <p>{{ mocktail.country }} | {{ mocktail.detail }}</p>
            </div>
            <span>{{ mocktail.price }}</span>
          </li>
        </ul>
      </div>
    </div>
  </section>
</template>

<style scoped></style>
