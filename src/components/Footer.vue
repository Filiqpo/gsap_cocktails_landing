<script setup>
import { openingHours, socials } from "../../constants";
import { onMounted } from "vue";
import gsap from "gsap";
import { ScrollTrigger, SplitText } from "gsap/all";

gsap.registerPlugin(SplitText, ScrollTrigger);

onMounted(() => {
  const titleSplit = SplitText.create("#contact h2", { type: "word" });

  const timeline = gsap.timeline({
    ScrollTrigger: {
      trigger: "#contact",
      start: "top center",
    },
    ease: "power1.inOut",
  });

  timeline.from(titleSplit.words, {
    opacity: 0,
    yPercent: 100,
    stagger: 0.02,
  });
  timeline.from("#contact h3, #contact p", {
    opacity: 0,
    yPercent: 100,
    stagger: 0.02,
  });
  timeline.to("#f-right-leaf", {
    y: "-50",
    duration: 1,
    ease: "power1.inOut",
  });
  timeline.to(
    "#f-left-leaf",
    {
      y: "-50",
      duration: 1,
      ease: "power1.inOut",
    },
    "<"
  );
});
</script>

<template>
  <footer id="contact">
    <img
      src="/images/footer-right-leaf.png"
      alt="leaf-right"
      id="f-right-leaf"
    />
    <img src="/images/footer-left-leaf.png" alt="leaf-left" id="f-left-leaf" />
    <div class="content">
      <h2>Where to find us</h2>
      <div class="">
        <h3>Visit Our Bar</h3>
        <p>456, Raq Blvd. #404, Los Angeles, CA 90210</p>
      </div>
      <div>
        <h3>Contact Us</h3>
        <p>(555) 987-6543</p>
        <p>hello@jsmcocktail.com</p>
      </div>
      <div>
        <h3>Open Every Day</h3>
        <p v-for="time in openingHours" :key="time.day">
          {{ time.day }} : {{ time.time }}
        </p>
      </div>
      <div>
        <h3>Socials</h3>
        <div class="flex-center gap-5">
          <a
            v-for="socials in socials"
            :key="socials.name"
            :href="socials.url"
            target="_blank"
            rel="noopener noreferrer"
            :aria-label="socials.name"
          >
            <img :src="socials.icon" alt="" />
          </a>
        </div>
      </div>
    </div>
  </footer>
</template>

<style scoped></style>
