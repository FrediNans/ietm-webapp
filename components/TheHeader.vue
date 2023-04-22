<template>
  <header>
    <div id="logo">
      <h1 class="text-center m-0">Images et Mouvements</h1>
    </div>
    <nav
      class="d-flex justify-content-between justify-content-lg-start align-items-center"
    >
      <h2 class="m-0 h5 d-lg-none">MENU</h2>
      <button
        type="button"
        class="btn m-0 px-2 py-0 d-lg-none"
        data-toggle="collapse"
        data-target="#mobileMenu"
        aria-expanded="false"
        aria-controls="mobileMenu"
      >
        <span class="material-icons-outlined h2 m-0">menu</span>
      </button>

      <nuxt-link
        v-for="link in links"
        :key="link.label"
        :to="link.to"
        class="d-none d-lg-flex px-2 py-3 text-decoration-none lg-links"
      >
        <span class="material-icons-outlined md-18 mx-2 links">
          {{ link.icon }}
        </span>
        <span class="links">{{ link.label }}</span></nuxt-link
      >
    </nav>
    <nav id="mobileMenu" class="collapse bg-white">
      <nuxt-link
        v-for="link in links"
        :key="link.label"
        class="links d-flex align-items-center py-2"
        :to="link.to"
        data-target="#mobileMenu"
        data-toggle="collapse"
        ><span class="material-icons-outlined mx-2"> {{ link.icon }} </span
        ><span> {{ link.label }} </span></nuxt-link
      >
    </nav>
  </header>
</template>

<script>
export default {
  data() {
    return {
      open: false,
      links: [
        {
          label: "Accueil",
          icon: "home",
          to: "/",
        },
        {
          label: "Qui sommes-nous ?",
          icon: "badge",
          to: "/about",
        },
        {
          label: "Festival",
          icon: "celebration",
          to: "/festival",
        },
        {
          label: "Stages",
          icon: "sports_gymnastics",
          to: "/stages",
        },
        {
          label: "Studio Onze",
          icon: "palette",
          to: "/studioonze",
        },
        {
          label: "Animations",
          icon: "diversity_1",
          to: "/animations",
        },
        {
          label: "Contact",
          icon: "contact_mail",
          to: "/contact",
        },
      ],
    }
  },
  methods: {},
}
</script>

<style lang="scss" scoped>
@font-face {
  font-family: "NasalizationRg-Regular";
  font-style: normal;
  font-weight: normal;
  src: local("NasalizationRg-Regular"),
    url("./assets/fonts/nasalization rg.woff") format("woff");
}
header {
  box-shadow: 0px 1px 9px 1px $secondary;
  width: 100%;
  background-color: $primary;
  z-index: 1000;
  position: fixed;
}
#logo {
  padding: 1rem;
  background-color: $secondary;
  color: white;
}
h1 {
  font-family: "NasalizationRg-Regular";
  font-size: 1.5rem;
  font-weight: bold;
}
nav {
  background-color: $primary;
  padding: 0 1rem 0 1rem;
  font-size: 1rem;
}
#mobile-menu {
  background-color: white;
  border-bottom: 1px solid $secondary;
  border-right: 1px solid $secondary;
  z-index: 5;
}
.links {
  color: $secondary;
  font-weight: 600;
}
.lg-links {
  transition: all 0.2s;
}
.lg-links:hover {
  background: rgb(228, 134, 244);
  background: radial-gradient(
    circle,
    rgba(228, 134, 244, 1) 0%,
    rgba(206, 147, 216, 1) 100%
  );
}

.v-enter-active,
.v-leave-active {
  transition: all 0.3s;
}

.v-enter-from,
.v-leave-to {
  transform: translateX(-1000px);
}
</style>
