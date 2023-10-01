<script setup>
/* import Banner from "../components/Banner.vue"; */
/* import Child from "../components/Child.vue"; */
import Animated from "../components/Animated.vue";
</script>

<template>
  <main>
    <!--  <Banner /> -->
    <!--  <Child /> -->
    <Animated />
  </main>
</template>

<script>
export default {
  mounted() {
    const observer = new IntersectionObserver((entries) => {
      entries.forEach((entry) => {
        console.log(entry);
        if (entry.isIntersecting) {
          entry.target.classList.add("show");
        } else {
          entry.target.classList.remove("show");
        }
      });
    });

    const hiddenElements = document.querySelectorAll(".hidden");
    hiddenElements.forEach((el) => observer.observe(el));
  },
};
</script>
