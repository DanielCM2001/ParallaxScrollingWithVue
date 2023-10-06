<template>
  <div>
    <header><h1 class="hidden">Scroll</h1></header>
    <section class="animation space">
      <div class="rocket-man-wrapper">
        <img src="../assets/images/Rocket2.png" class="rocket-man" alt="" />
      </div>
      <div class="world">
        <img src="../assets/images/WorldX4.png" alt="" class="world-world" />
      </div>
      <h1 class="GlowLabel">
        I enjoy creating things that live
        <br />
        on the internet...
      </h1>
    </section>
    <section class="animation sky-inside-world"></section>
    <section class="animation bg-section">Content for the next section</section>
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
          y: -window.innerHeight,
        },
      ],
    };

    const tween = new TimelineLite();

    // First, the flight path animation for the rocket
    tween.add(
      TweenLite.to(".rocket-man", 1, {
        bezier: flightPath,
        ease: Power1.easeInOut,
      })
    );

    // Then, add a scaling effect for the world at the end of the rocket animation
    tween.add(
      TweenLite.to(".world", 1, {
        scale: 5,
        ease: Linear.easeNone,
        onComplete: goToNextSection,
      })
    );

    tween.add(
      TweenLite.to(".world-world", 1, {
        opacity: 0,
        ease: Power1.easeInOut,
      })
    );

    // Finally, add a fade-in effect for the sky inside the world

    // Create a ScrollMagic controller
    const controller = new ScrollMagic.Controller();

    // Create a ScrollMagic scene
    const scene = new ScrollMagic.Scene({
      triggerElement: ".animation",
      duration: 1000, // Adjust the duration as needed
      triggerHook: 0,
    })
      .setTween(tween)
      .setPin(".animation")
      .addTo(controller);

    function goToNextSection() {
      // Transition to the next section (e.g., when the plane zoom-in animation is complete)
      const nextSection = document.querySelector(".sky-inside-world");
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
  left: 25%;
  animation: pump 1.5s infinite alternate;
}

.world {
  position: absolute;
  height: 100vh;
  width: 100%;
  bottom: 0;
  left: 0;
  z-index: 1;
}

.world-world {
  position: absolute;
  height: 400px;
  bottom: 0%;
  left: 25%;
  z-index: 1;
}

.sky-inside-world {
  height: 100vh;
  width: 100%;
  background: linear-gradient(180deg, #000514 0%, #03a9f4 80%);
}

.GlowLabel {
  color: #c940eb;
  text-align: center;
  text-shadow: 0px 4px 50px #c940eb;
  font-family: Poppins;
  font-size: 80px;
  font-style: normal;
  font-weight: 400;
  line-height: normal;
}

@keyframes pump {
  0% {
    transform: translateY(0);
  }
  100% {
    transform: translateY(-20px);
  }
}
</style>
