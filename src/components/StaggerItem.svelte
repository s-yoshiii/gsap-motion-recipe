<script lang="ts">
  import { gsap } from "gsap";
  import { onMount } from "svelte";
  import SectionLayout from "./SectionLayout.svelte";
  onMount(() => {
    gsap.from("li", {
      y: 10,
      autoAlpha: 0,
      duration: 1,
      ease: "power4.out",
      stagger: 0.1,
    });
  });
</script>

<SectionLayout cl="stagger">
  <h2>Stagger</h2>
  <div class="cont">
    <ul>
      <li>1</li>
      <li>2</li>
      <li>3</li>
      <li>4</li>
      <li>5</li>
      <li>6</li>
      <li>7</li>
      <li>8</li>
      <li>9</li>
      <li>10</li>
      <li>11</li>
      <li>12</li>
      <li>13</li>
      <li>14</li>
      <li>15</li>
      <li>16</li>
      <li>17</li>
      <li>18</li>
    </ul>
  </div>
</SectionLayout>

<style lang="scss">
  @use "../assets/variable";
  ul {
    display: grid;
    grid-template-columns: repeat(auto-fit, 100px);
    grid-auto-rows: 100px;
    justify-content: center;
    gap: 10px;
    li {
      display: flex;
      justify-content: center;
      align-items: center;
      &:nth-child(3n + 1) {
        background: variable.$stagger-color01;
      }
      &:nth-child(3n + 2) {
        background: variable.$stagger-color02;
      }
      &:nth-child(3n) {
        background: variable.$stagger-color03;
      }
    }
  }
</style>
