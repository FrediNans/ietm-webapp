<template>
  <div class="baner p-3 p-lg-0">
    <div
      class="d-flex flex-column align-items-center flex-lg-row justify-content-lg-between p-lg-0"
    >
      <div class="baner__title my-5 col-lg-8">
        <h1 class="h3">{{ pageTitle }}</h1>
        <h2 class="h4" v-if="pageTitle2.length > 0">{{ pageTitle2 }}</h2>
      </div>
      <div
        class="col-12 col-md-8 col-lg-4 p-lg-0 d-lg-flex justify-content-center"
      >
        <img :src="imgUrl" :alt="imgTextAlt" class="baner__img img-fluid" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["pageTitle", "pageTitle2", "imgUrl", "imgTextAlt"],
}
</script>

<style lang="scss" scoped>
.baner {
  background-color: $primaryDark;
  color: white;
  &__title {
    text-align: center;
  }
  &__img {
    border: 5px solid white;
    border-radius: 15px;
    margin-bottom: -100px;
  }
}
@media (min-width: 992px) {
  .baner {
    &__img {
      margin-bottom: 0;
      border: none;
      border-radius: 0;
    }
  }
}
</style>
