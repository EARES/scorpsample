<template>
  <section class="section">
    <div class="container">
      <div class="columns">
        <div class="column">
          <h1 class="title">Home</h1>
          <p>{{ $t("message.lorem") }}</p>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'Home',
};
</script>

<style scoped>
.section {
  min-height: 83vh;
}
</style>
