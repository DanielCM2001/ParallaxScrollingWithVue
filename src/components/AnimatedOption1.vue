<template>
  <div>
    <header><h1 class="hidden">Scroll</h1></header>
    <section class="animation space">
      <div class="rocket-man-wrapper">
        <img src="../assets/images/Rocket2.png" class="rocket-man" alt="" />
      </div>
      <img src="../assets/images/WorldX4.png" class="world" alt="" />
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
      autoRotate: false,
      values: [
        {
          x: 0,
          y: -50,
        },
        {
          x: 0,
          y: -100,
        },
        {
          x: 0,
          y: -150,
        },
        {
          x: 0,
          y: -200,
        },
        {
          x: 0,
          y: -250,
        },
        {
          x: 0,
          y: -window.innerHeight,
        },
      ],
    };

    const tween = new TimelineLite();

    // First, the flight path animation
    tween.add(
      TweenLite.to(".rocket-man", 1, {
        bezier: flightPath,
        ease: Power1.easeInOut,
        onComplete: goToNextSection,
      })
    );

    // Then, add a scaling effect at the end
    tween.add(
      TweenLite.fromTo(
        ".world",
        1,
        { scale: 1 }, // Start with the current scale

        { scale: 5, onComplete: goToNextSection } // End with a smaller scale and trigger transition
      )
    );

    /*  tween.add(
      TweenLite.fromTo(
        ".world",
        10,
        { scale: 1 },
        { scale: 8, ease: Linear.easeNone, repeat: -1 }
      )
    ); */

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

.rocket-man-wrapper {
  position: absolute;
  top: 50%;
  left: 25%; /* Position on the right */
  animation: pump 1.5s infinite alternate;
}

.world {
  position: absolute;
  height: 400px;
  bottom: 0%;
  left: 25%;
  z-index: 1;
}

.ovni {
  position: absolute;
  height: 300px;
  top: 0%;
  left: 0%;
  z-index: 1;
}

@keyframes pump {
  0% {
    transform: translateY(0px);
  }
  100% {
    transform: translateY(-20px);
  }
}

@media screen and (max-width: 600px) {
  .rocket-man-wrapper {
    position: absolute;
    top: 50%;
    left: 0%; /* Position on the right */
    animation: pump 1.5s infinite alternate;
  }

  .world {
    position: absolute;
    height: 400px;
    bottom: 0%;
    left: 0%;
    z-index: 1;
  }
}
</style>
