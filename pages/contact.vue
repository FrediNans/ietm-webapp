<template>
  <div>
    <PageBaner
      pageTitle="CONTACT"
      pageTitle2=""
      imgUrl="../images/phone.webp"
      imgTextAlt="Stage 2020, cours de réveil corporel, conduit par Henri Charbonnier."
    />
    <div class="spacer"></div>
    <div class="p-3">
      <p class="text-justify">
        Pour toutes questions ou demande d'information vous pouvez nous
        contacter :
      </p>
      <ul>
        <li>
          <strong>Par courrier :</strong><br />
          Association Images et Mouvements<br />
          11 rue Michel le Comte<br />
          75003 Paris
        </li>
        <li>
          <strong>Par mail :</strong><br /><a
            href="mailto:asso.imagesetmouvements@gmail.com"
            >asso.imagesetmouvements@gmail.com</a
          >
        </li>
        <li>
          <strong>Par téléphone :</strong><br /><a href="tel:+33663747259">
            06 63 74 72 59
          </a>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  head() {
    return {
      meta: [
        {
          name: "description",
          content:
            "Tout les moyens que l'association Images et Mouvements met à disposition pour que l'on puisse les contacter.",
        },
      ],
    }
  },
}
</script>

<style lang="scss" scoped>
.spacer {
  height: 150px;
}
@media (min-width: 992px) {
  .spacer {
    height: 50px;
  }
}
</style>
