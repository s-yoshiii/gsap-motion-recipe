<script lang="ts">
  import { gsap } from "gsap";
  import { onMount } from "svelte";
  import SectionLayout from "./SectionLayout.svelte";
  import { ScrollTrigger } from "gsap/dist/ScrollTrigger";
  gsap.registerPlugin(ScrollTrigger);
  let contInner: HTMLDivElement;

  onMount(() => {
    // gsap.to(".box", {
    //   x: "70vw",
    //   rotation: 360,
    //   duration: 3,
    //   scrollTrigger: {
    //     trigger: ".box",
    //     start: "top bottom",
    //     end: "bottom top",
    //     toggleActions: "play none none reset",
    //     markers: true,
    //     id: "box",
    //     //scrub: true,
    //     scrub: 0.5, // smoothing
    //   },
    // });8
    const sentences = [...contInner.querySelectorAll("p")];
    for (const item of sentences) {
      let output = "";
      const content = item.innerHTML.replace(/<br\s*\/?>/gi, "\n");
      for (const str of content.split("")) {
        output += str.match(/\r\n/g) ? "<br>" : `<span>${str}</span>`;
      }
      item.innerHTML = output;
    }
  });
</script>

<SectionLayout cl="scroll">
  <h2>Scroll Trigger</h2>
  <div class="cont">
    <div class="cont__inner" bind:this={contInner}>
      <p>
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Maxime
        molestias, nam atque quam doloribus temporibus eaque impedit! Suscipit
        facilis quasi esse! Hic doloribus provident placeat a perferendis
        consequatur soluta animi.
      </p>
      <p>
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Maxime
        molestias, nam atque quam doloribus temporibus eaque impedit! Suscipit
        facilis quasi esse! Hic doloribus provident placeat a perferendis
        consequatur soluta animi.
      </p>
    </div>
  </div>
</SectionLayout>

<style lang="scss">
  .cont {
    &__inner {
      padding: 1rem;
    }
    & p {
      font-size: 18px;
      font-size: 1.8rem;
      line-height: 2;
    }
  }
</style>
