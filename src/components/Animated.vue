<template>
  <div>
    <header><h1 class="hidden">Scroll</h1></header>
    <section class="animation space">
      <img src="../assets/images/RocketMan.png" class="paper-plane" alt="" />
      <img src="../assets/images/World.png" class="world" alt="" />
    </section>
    <section class="animation bg-section">
      <img src="../assets/images/Sky.png" class="Sky" alt="" />
    </section>
    <footer><h1 class="hidden">Wooow</h1></footer>
  </div>
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
      ],
    };

    const tween = new TimelineLite();

    // First, the flight path animation
    tween.add(
      TweenLite.to(".paper-plane", 1, {
        bezier: flightPath,
        ease: Power1.easeInOut,
      })
    );

    // Then, add a scaling effect at the end
    tween.add(
      TweenLite.fromTo(
        ".world",
        1,
        { scale: 1 }, // Start with the current scale

        { scale: 80, onComplete: goToNextSection } // End with a smaller scale and trigger transition
      )
    );

    const controller = new ScrollMagic.Controller();

    const scene = new ScrollMagic.Scene({
      triggerElement: ".animation",
      duration: 1000,
      triggerHook: 0,
    })
      .setTween(tween)
      .setPin(".animation")
      .addTo(controller);

    function goToNextSection() {
      // Transition to the next section (e.g., when the plane zoom-in animation is complete)
      const nextSection = document.querySelector(".bg-section");
      window.scrollTo({
        top: nextSection.offsetTop,
        behavior: "smooth",
      });
    }
  },
};
</script>

<style scoped>
.animation {
  position: relative;
  height: 100vh;
  overflow: hidden;
}

.space {
  background-image: url("../assets/images/SpaceBackground.png");

  height: 100vh;
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  display: flex;
  align-items: center;
  justify-content: center;
}

.bg-section {
  height: 100vh;
  background-image: url("../assets/images/Sky.png");
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  display: flex;
  align-items: center;
  justify-content: center;
}

.paper-plane {
  position: absolute;
  height: 100px;
  top: 50%;
  left: 0;
  z-index: 1;
}
.world {
  position: absolute;
  height: 400px;
  bottom: 0%;
  left: 25%;
  z-index: 1;
}
</style>
