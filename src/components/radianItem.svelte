<script lang="ts">
  import { gsap } from "gsap";
  import { onMount } from "svelte";
  import SectionLayout from "./SectionLayout.svelte";
  const params = { radian: 0 };
  onMount(() => {
    gsap.to(params, {
      radian: Math.PI * 2,
      duration: 5,
      ease: "power4.inOut",
      onUpdate: () => {
        const { radian } = params;
        const x = Math.cos(radian) * 100;
        const y = Math.sin(radian) * 100;
        gsap.set(".circle", { x, y });
      },
      repeat: -1,
      repeatDelay: 1,
    });
  });
</script>

<SectionLayout cl="radian">
  <h2>Radian</h2>
  <div class="cont">
    <div class="cont__inner">
      <div class="circle" />
    </div>
    <div class="cont__inner">
      <div class="circle" />
    </div>
    <div class="cont__inner">
      <div class="circle" />
    </div>
    <div class="cont__inner">
      <div class="circle" />
    </div>
    <div class="cont__inner">
      <div class="circle" />
    </div>
  </div>
</SectionLayout>

<style lang="scss">
  @use "../assets/variable";
  .cont {
    display: grid;
    grid-template-columns: repeat(auto-fill, 200px);
    min-height: 400px;
    &__inner {
      height: 200px;
      width: 200px;
      transform: translate(50%, 50%);
    }
  }
  .circle {
    position: absolute;
    background: variable.$radian-color;
    width: 20px;
    height: 20px;
    border-radius: 50%;
  }
</style>
