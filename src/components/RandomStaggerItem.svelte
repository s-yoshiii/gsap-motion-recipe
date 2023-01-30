<script lang="ts">
  import { gsap } from "gsap";
  import SectionLayout from "./SectionLayout.svelte";
  import { onMount } from "svelte";
  const colors = ["#fffbac", "#ffd495", "#faab78"];
  const chooseColor = <T>(array: T[]) => {
    const arrayIndex = Math.floor(Math.random() * array.length);
    return colors[arrayIndex];
  };
  let settings: string[] = [];
  for (let i = 0; i < 500; i++) {
    const colorClass = chooseColor(colors);
    settings.push(colorClass);
  }
  onMount(() => {
    gsap.to(".cont__item", {
      y: "100vh",
      duration: 2,
      ease: "bounce.out",
      stagger: {
        each: 0.01,
        from: "random",
        grid: "auto",
        repeat: -1,
      },
    });
  });
</script>

<SectionLayout cl="random">
  <h2>Randam Stagger</h2>
  <div class="cont">
    {#each settings as value}
      <div class="cont__item" style:background={value} />
    {/each}
  </div>
</SectionLayout>

<style lang="scss">
  @use "../assets/variable";
  .cont {
    display: grid;
    grid-template-columns: repeat(auto-fill, 20px);
    grid-auto-rows: 20px;
    gap: 10px;
    min-height: 100vh;
    overflow: hidden;
    &__item {
      width: 20px;
      height: 20px;
      border-radius: 50%;
    }
  }
</style>
