<template>
  <header><h1 class="hidden">Scroll</h1></header>
  <!--  <section class="animation">
    <img src="../assets/images/paper.png" alt="" />
  </section>
  <footer><h1 class="hidden">Wooow</h1></footer> -->
</template>

<script>
export default {
  mounted() {
    const flightPath = {
      curviness: 1.25,
      autoRotate: true,
      values: [
        {
          x: 100,
          y: -20,
        },
        {
          x: 300,
          y: 10,
        },

        {
          x: 350,
          y: -50,
        },
        {
          x: 600,
          y: 100,
        },
        {
          x: 300,
          y: 10,
        },
        {
          x: window.innerWidth,
          y: -250,
        },
      ],
    };

    const tween = new TimelineLite();

    tween.add(
      TweenLite.to(".paper-plane", 1, {
        bezier: flightPath,
        ease: Power1.easeInOut,
      })
    );

    const controller = new ScrollMagic.Controller();

    const scene = new ScrollMagic.Scene({
      triggerElement: ".animation",
      duration: 1000,
      triggerHook: 0,
    })
      .setTween(tween)
      /* .addIndicators() */
      .setPin(".animation")
      .addTo(controller);
  },
};
</script>

<style scoped>
.animation {
  position: relative;
  height: 100vh;
  overflow: hidden;
}

.paper-plane {
  position: absolute;
  height: 100px;
  top: 50%;
  left: 0;
}
</style>
