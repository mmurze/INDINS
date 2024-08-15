<template>
  <section>
    <div class="wrapper">
      <slot/>
    </div>
  </section>
</template>

<script setup>

</script>

<style lang="scss">
p{
  margin: 0;
  padding: 0;
}
.wrapper {
  width: 100%;
  max-width: 1200px;
  margin: 0 auto ;
  padding: 0 15px;
  font-size: 18px;
  font-family: Roboto,serif;
  box-sizing: border-box;
}

@media (max-width: 600px) {
  .wrapper{
    font-size: 15px;
  }
}
</style>
