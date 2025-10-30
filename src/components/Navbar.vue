<script setup>
import { navLinks } from "../../constants";
import gsap from "gsap";
import { ScrollTrigger } from "gsap/all";
import { onMounted } from "vue";

gsap.registerPlugin(ScrollTrigger);

onMounted(() => {
  const tl = gsap.timeline({
    scrollTrigger: {
      trigger: "nav",
      start: "bottom top",
    },
  });

  tl.fromTo(
    "nav",
    { backgroundColor: "transparent" },
    {
      backgroundColor: "#00000050",
      backgroundFilter: "blur(10px)",
      duration: 1,
      ease: "power1.inOut",
    }
  );
});
</script>

<template>
  <nav>
    <div>
      <a href="#home" class="flex items-center gap-2">
        <img src="/public/images/logo.png" alt="logo" />
        <p>Velvet Pour</p>
      </a>

      <ul>
        <li v-for="link in navLinks" :key="link.id" class="nav-link">
          <a :href="`#${link.id}`">{{ link.title }}</a>
        </li>
      </ul>
    </div>
  </nav>
</template>

<style scoped></style>
