<script lang="ts">
  import { gsap } from "gsap";
  import { onMount } from "svelte";
  import SectionLayout from "./SectionLayout.svelte";
  import { ScrollTrigger } from "gsap/dist/ScrollTrigger";
  gsap.registerPlugin(ScrollTrigger);
  let cont: HTMLDivElement;

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
    // });
    const sentences = [...cont.querySelectorAll("p")];
    for (const item of sentences) {
      let output = "";
      const content = item.innerHTML.replace(/<br\s*\/?>/gi, "\n");
      for (const str of content.split("")) {
        output += str.match(/\r\n/g) ? "<br>" : `<span>${str}</span>`;
      }
      item.innerHTML = output;
    }
    let q = gsap.utils.selector(cont);
    let boxes = q(".cont__inner");
    boxes.forEach((box) => {
      const tl = gsap.timeline({
        scrollTrigger: {
          trigger: box,
          start: "top bottom -=20",
          toggleActions: "restart none none none", // onEnter, onLeave, onEnterBack, onLeaveBack
          // markers: true,
        },
      });

      tl.from(box, {
        opacity: 0,
        y: 20,
      });
      tl.from(
        gsap.utils.toArray("span", box),
        {
          opacity: 0,
          duration: 0.01,
          stagger: 0.005,
        },
        "-=1"
      );
    });
  });
</script>

<SectionLayout cl="scroll">
  <h2>Scroll Trigger</h2>
  <div class="cont" bind:this={cont}>
    <div class="cont__sect">
      <div class="cont__inner">
        <p>
          aaaaaaaaaaaaaaaaaaaaLorem ipsum dolor sit amet consectetur adipisicing
          elit. Maxime molestias, nam atque quam doloribus temporibus eaque
          impedit! Suscipit facilis quasi esse! Hic doloribus provident placeat
          a perferendis consequatur soluta animi.
        </p>
        <p>
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Maxime
          molestias, nam atque quam doloribus temporibus eaque impedit! Suscipit
          facilis quasi esse! Hic doloribus provident placeat a perferendis
          consequatur soluta animi.
        </p>
      </div>
    </div>
    <div class="cont__sect">
      <div class="cont__inner">
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
    <div class="cont__sect">
      <div class="cont__inner">
        <p>
          33333Lorem ipsum dolor sit amet consectetur adipisicing elit. Maxime
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
  </div>
</SectionLayout>

<style lang="scss">
  @use "../assets/variable";
  .cont {
    $parent: &;
    & + & {
      margin-top: 100px;
    }
    &__sect {
      display: flex;
      & + & {
        margin-top: 100px;
      }
      &:nth-of-type(2n) {
        justify-content: flex-end;
        #{$parent}__inner {
          background: variable.$scroll-color02;
        }
      }
      &:nth-of-type(3n) {
        #{$parent}__inner {
          background: variable.$scroll-color03;
        }
      }
    }
    &__inner {
      padding: 2rem;
      display: inline-block;
      background: variable.$scroll-color01;
    }
    & p {
      font-size: 18px;
      font-size: 1.8rem;
      line-height: 2;
    }
  }
</style>
