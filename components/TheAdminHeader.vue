<template>
  <div>
    <header>
      <div id="logo">
        <h1 class="text-center m-0">Images et Mouvements</h1>
      </div>
    </header>
    <nav class="d-flex align-items-center justify-content-between bg-light">
      <h1 class="h3 mx-5">Panel administrateur</h1>
      <div class="d-flex mx-5">
        <nuxt-link class="d-flex px-3 py-3 text-decoration-none lg-links" to="/"
          >Retour sur le site</nuxt-link
        >
        <nuxt-link
          class="d-flex px-3 py-3 text-decoration-none lg-links"
          to="/adminactus"
          >Actualités</nuxt-link
        >
        <nuxt-link
          class="d-flex px-3 py-3 text-decoration-none lg-links"
          to="/adminstages"
          >Stages</nuxt-link
        >
      </div>
    </nav>
  </div>
</template>

<style lang="scss" scoped>
#logo {
  padding: 1rem;
  background-color: $secondary;
  color: white;
}
.lg-links {
  color: $secondary;
  font-weight: 600;
  font-size: 1rem;
}
</style>
