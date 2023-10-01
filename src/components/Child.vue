<template>
  <header><h1 class="hidden">Child</h1></header>
  <section class="childAnimation">
    <div class="paper-plane-wrapper">
      <img
        class="child-paper-plane"
        src="../assets/images/paper.png"
        alt="child-paper-plane"
      />
    </div>
    <div class="rocket-man-wrapper">
      <img
        class="child-rocket"
        src="../assets/images/RocketMan.png"
        alt="child-rocket"
      />
    </div>
  </section>
  <footer><h1>WooooW</h1></footer>
</template>

<script>
export default {
  mounted() {
    // Your GSAP animation code
    const paperFlightPath = {
      curviness: 1.25,
      autoRotate: true,
      values: [
        // Define the flight path for the paper-plane (left to right)
        {
          x: 100,
          y: -20,
        },
        {
          x: 300,
          y: 100,
        },
        {
          x: 500,
          y: 150,
        },
        {
          x: 550,
          y: 200,
        },
        {
          x: 600,
          y: 250,
        },
        {
          x: window.innerWidth,
          y: 300,
        },
      ],
    };

    const rocketFlightPath = {
      curviness: 1.25,
      autoRotate: false,
      values: [
        // Define the flight path for the rocket (right to left)
        {
          x: -200,
          y: -50,
        },
        {
          x: -350,
          y: -150,
        },
        {
          x: -550,
          y: -200,
        },
        {
          x: -600,
          y: -250,
        },
        {
          x: -650,
          y: -300,
        },
        {
          x: -window.innerWidth,
          y: -450,
        },
      ],
    };

    const paperTween = new TimelineLite();
    paperTween.add(
      TweenLite.to(".child-paper-plane", 1, {
        bezier: paperFlightPath,
        ease: Power1.easeInOut,
      })
    );

    const rocketTween = new TimelineLite();
    rocketTween.add(
      TweenLite.to(".child-rocket", 1, {
        bezier: rocketFlightPath,
        ease: Power1.easeInOut,
      })
    );

    const controller = new ScrollMagic.Controller();

    const paperScene = new ScrollMagic.Scene({
      triggerElement: ".childAnimation",
      duration: 1000,
      triggerHook: 0,
    })
      .setTween(paperTween)
      .setPin(".childAnimation")
      .addTo(controller);

    const rocketScene = new ScrollMagic.Scene({
      triggerElement: ".childAnimation",
      duration: 1000,
      triggerHook: 0,
    })
      .setTween(rocketTween)
      /*   .setPin(".childAnimation") */
      .addTo(controller);
  },
};
</script>

<style scoped>
.childAnimation {
  position: relative;
  height: 100vh;
  overflow: hidden;
  background-color: palegoldenrod;
}

.paper-plane-wrapper {
  position: absolute;
  /*   height: 100px; */
  top: 50%;
  left: 0; /* Position on the left */
  animation: pump 1.5s infinite alternate;
}

.rocket-man-wrapper {
  position: absolute;
  /*  height: 100px; */
  top: 50%;
  right: 0; /* Position on the right */
  animation: pump 1.5s infinite alternate;
}

.child-paper-plane {
  /* No need to set left here, it's positioned by the wrapper */
  height: 100px;
}

.child-rocket {
  /* No need to set right here, it's positioned by the wrapper */
  height: 100px;
}

@keyframes pump {
  0% {
    transform: translateY(0px);
  }
  100% {
    transform: translateY(-20px);
  }
}
</style>
