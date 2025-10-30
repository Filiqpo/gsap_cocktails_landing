<script setup>
import { ref, onMounted } from "vue";
import gsap from "gsap";
import { ScrollTrigger, SplitText } from "gsap/all";

gsap.registerPlugin(ScrollTrigger, SplitText);
</script>

<template>
  <div class="flex-center h-screen">Hello World</div>
</template>

<style scoped></style>
