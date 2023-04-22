<template>
  <div>
    <TheHeader />
    <div id="spacer"></div>
    <Nuxt />
    <TheFooter />
  </div>
</template>

<style lang="scss">
body {
  margin: 0;
  padding: 0;
}

#spacer {
  height: 105px;
}
@media (min-width: 992px) {
  #spacer {
    height: 117px;
  }
}
.page-enter-active,
.page-leave-active {
  transition: all 0.3s;
}
.page-enter,
.page-leave-to {
  transform: translateX(-500px);
  opacity: 0;
}
</style>
