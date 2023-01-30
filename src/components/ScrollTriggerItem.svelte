<script lang="ts">
  import { gsap } from "gsap";
  import { onMount } from "svelte";
  import SectionLayout from "./SectionLayout.svelte";
  import { ScrollTrigger } from "gsap/ScrollTrigger";
  gsap.registerPlugin(ScrollTrigger);
  onMount(() => {
    gsap.to(".box", {
      x: "70vw",
      rotation: 360,
      duration: 3,

      scrollTrigger: {
        trigger: ".box",
        start: "top bottom",
        end: "bottom top",
        toggleActions: "play none none reset",
        markers: true,
        id: "box",
        //scrub: true,
        scrub: 0.5, // smoothing
      },
    });
  });
</script>

<SectionLayout cl="scroll">
  <div class="box" />
</SectionLayout>

<style lang="scss">
  .box {
    width: 50px;
    height: 50px;
    background: #6fb936;
    border-radius: 10px;
  }
</style>
