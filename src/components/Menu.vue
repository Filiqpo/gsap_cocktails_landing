<script setup>
import { onMounted, ref, computed, watch } from "vue";
import { sliderLists } from "../../constants/index";
import gsap from "gsap";

onMounted(() => {
  watch(currentIndex, () => {
    gsap.fromTo("#title", { opacity: 0 }, { opacity: 1, duration: 2 });
    gsap.fromTo(
      ".cocktail img",
      { opacity: 0, xPercent: -100 },
      {
        xPercent: 0,
        opacity: 1,
        ease: "power1.inOut",
      }
    );
    gsap.fromTo(
      ".details h2",
      {
        yPercent: 100,
        opacity: 0,
      },
      {
        yPercent: 0,
        opacity: 100,
        ease: "power1.inOut",
      }
    );
    gsap.fromTo(
      ".details p",
      {
        yPercent: 100,
        opacity: 0,
      },
      {
        yPercent: 0,
        opacity: 100,
        ease: "power1.inOut",
      }
    );
  });
});
const currentIndex = ref(0);
const totalCocktails = sliderLists.length;
const contentRef = ref(null);

const goToSlide = (index) => {
  const newIndex = (index + totalCocktails) % totalCocktails;
  currentIndex.value = newIndex;
};

const getCocktailAt = (indexOffset) => {
  return sliderLists[
    (currentIndex.value + indexOffset + totalCocktails) % totalCocktails
  ];
};

const currentCocktail = computed(() => getCocktailAt(0));
const prevCocktail = computed(() => getCocktailAt(-1));
const nextCocktail = computed(() => getCocktailAt(1));
</script>

<template>
  <section id="menu" aria-labelledby="menu-heading">
    <img src="/images/slider-left-leaf.png" alt="left-leaf" id="m-left-leaf" />
    <img
      src="/images/slider-right-leaf.png"
      alt="right-leaf"
      id="m-right-leaf"
    />

    <h2 id="menu-heading" class="sr-only">Cocktail menu</h2>

    <nav class="cocktail-tabs" aria-label="Cocktail Navigation">
      <button
        v-for="(cocktail, index) in sliderLists"
        :key="cocktail.name"
        :class="[
          index === currentIndex
            ? 'text-white border-white'
            : 'text-white/50 border-white/50',
        ]"
        @click="goToSlide(index)"
      >
        {{ cocktail.name }}
      </button>
    </nav>
    <div class="content">
      <div class="arrows">
        <button class="text-left" @click="goToSlide(currentIndex - 1)">
          <span>{{ prevCocktail.name }}</span>
          <img
            src="/images/right-arrow.png"
            alt="right-arrow"
            aria-hidden="true"
          />
        </button>
        <button class="text-left" @click="goToSlide(currentIndex + 1)">
          <span>{{ nextCocktail.name }}</span>
          <img
            src="/images/left-arrow.png"
            alt="left-arrow"
            aria-hidden="true"
          />
        </button>
      </div>
      <div class="cocktail">
        <img :src="currentCocktail.image" class="object-contain" alt="" />
      </div>
      <div class="recipe">
        <div :ref="contentRef" class="info">
          <p>Recipe for:</p>
          <p id="title">{{ currentCocktail.name }}</p>
        </div>
        <div class="details">
          <h2>{{ currentCocktail.title }}</h2>
          <p>{{ currentCocktail.description }}</p>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped></style>
