<template>
  <footer>
    <div class="d-flex justify-content-around p-3 col-6 mx-auto">
      <a href="mailto:asso.imagesetmouvements@gmail.com"
        ><span class="material-icons-outlined md-18 mx-2 links">
          email
        </span></a
      >
      <a href="tel:+33663747259"
        ><span class="material-icons-outlined"> local_phone </span></a
      >
    </div>
    <div class="p-3">
      <nuxt-link to="/legal"
        >Mentions légales et politique de confidentialité</nuxt-link
      >
    </div>
  </footer>
</template>

<style lang="scss" scoped>
footer {
  background-color: $secondary;
}
a {
  color: $primaryLight;
}
</style>
