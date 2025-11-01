<script setup>
import { ref, onMounted } from "vue";
import gsap from "gsap";
import { ScrollTrigger, SplitText } from "gsap/all";
import Navbar from "./components/Navbar.vue";
import Hero from "./components/Hero.vue";

gsap.registerPlugin(ScrollTrigger, SplitText);
</script>

<template>
  <main>
    <Navbar />
    <Hero />
  </main>
</template>

<style scoped></style>
