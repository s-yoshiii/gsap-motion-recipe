<script lang="ts">
  export let cl: string | null;
</script>

<section class={cl ? cl : ""}>
  <div>
    <slot props={cl} />
  </div>
</section>

<style lang="scss">
  @use "../assets/variable";
  section {
    padding: 70px 0;
    & > div {
      margin: 0 auto;
      max-width: 1080px;
      padding: 0 50px;
    }
  }
  .stagger {
    background: variable.$stagger-bg;
  }
  .random {
    background: variable.$random-bg;
  }
  .radian {
    background: variable.$radian-bg;
  }
</style>
