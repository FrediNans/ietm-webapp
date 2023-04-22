<template>
  <div class="p-3 d-md-flex flex-md-column align-items-md-center">
    <div class="col-md-10 col-xl-8">
      <h1 class="formInscription-title h3 mt-3 text-center">
        Formulaire d'inscription
      </h1>
      <p class="text-justify">
        Merci de remplir ce formulaire d'inscription ainsi que l'autorisation
        parentale, de les télécharger et de nous les retourner signer.<br />
        Vous pouvez aussi télécharger les documents vierges et les remplir
        manuellement en cliquant sur le bouton en bas de page.
      </p>
      <p>
        Par courrier :<br />
        Association Images et Mouvements 11 rue Michel le Comte 75003 Paris
      </p>
      <p>
        Par mail :<br />
        <a :href="mail">asso.imagesetmouvements@gmail.com</a>
      </p>
      <p class="text-justify font-italic">
        Aucune donnée de ce formulaire n'est conservée ou utilisée à des fins
        commerciales, elles sont complètement supprimées après le téléchargement
        du document.
      </p>
      <h2 class="formInscription-title h4 text-center">
        {{ stageName }}
      </h2>
      <p class="text-center">
        Du {{ convertDate(startDate) }} au {{ convertDate(endDate) }}
      </p>
    </div>
    <form class="d-lg-flex col-lg-8">
      <div class="col-lg-6">
        <div class="d-flex flex-column pb-3">
          <label for="childName">Nom et prénom de l'élève</label>
          <input id="childName" type="text" v-model="childName" />
        </div>
        <div class="d-flex flex-column pb-3">
          <label for="childBirthDate">Date de naissance de l'élève</label>
          <input id="childBirthDate" type="date" v-model="childBirthDate" />
        </div>
        <div class="d-flex flex-column pb-3">
          <label for="bloodGroup">Groupe sanguin de l'élève</label>
          <select
            class="form-control"
            id="exampleFormControlSelect1"
            v-model="bloodGroup"
          >
            <option>O+</option>
            <option>O-</option>
            <option>A+</option>
            <option>A-</option>
            <option>B+</option>
            <option>B-</option>
            <option>AB+</option>
            <option>AB-</option>
          </select>
        </div>
        <div class="d-flex flex-column pb-3">
          <label for="childSpecialEat">Régime alimentaire particulier</label>
          <input id="childSpecialEat" type="text" v-model="childSpecialEat" />
        </div>
        <div class="d-flex flex-column pb-3">
          <label for="parentName">Nom et prénom des parents</label>
          <input id="parentName" type="text" v-model="parentName" />
          <input
            class="mt-3"
            id="parentName2"
            type="text"
            v-model="parentName2"
          />
        </div>
      </div>
      <div class="col-lg-6">
        <div class="d-flex flex-column pb-3">
          <label for="adress">Adresse</label>

          <input id="adress" type="text" v-model="adress" />
        </div>
        <div class="d-flex flex-column pb-3">
          <label for="zip">Code postal</label>
          <input id="zip" type="text" v-model="zip" />
        </div>
        <div class="d-flex flex-column pb-3">
          <label for="city">Ville</label>
          <input id="city" type="text" v-model="city" />
        </div>
        <div class="d-flex flex-column pb-3">
          <label for="phoneNumber">N° de téléphone des parents</label>
          <input id="phoneNumber" type="tel" v-model="phoneNumber" />
        </div>
        <div class="d-flex flex-column pb-3">
          <label for="email">Email des parents</label>
          <input id="email" type="mail" v-model="email" />
        </div>
        <div class="d-flex flex-column pb-3">
          <label for="mobileNumber"
            >N° de portable des parents à prevenir en cas d'urgence</label
          >
          <input id="mobileNumber" type="tel" v-model="mobileNumber" />
          <input
            class="mt-3"
            id="mobileNumber2"
            type="tel"
            v-model="mobileNumber2"
          />
        </div>
        <button
          type="button"
          class="btn btn-success"
          @click="createPdf()"
          data-toggle="modal"
          data-target="#confirmModal"
        >
          Télécharger les documents
        </button>
      </div>
    </form>
    <div
      class="modal fade"
      id="confirmModal"
      tabindex="-1"
      aria-labelledby="exampleModalLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLabel">Inscription</h5>
          </div>
          <div class="modal-body">
            Vos documents sont prêts !<br />
            Nb: Pour nous les transmettre, vous pouvez retrouver nos coordonnées
            sur la page contact de notre site. Merci
          </div>
          <div class="modal-footer">
            <nuxt-link
              type="button"
              class="btn btn-primary"
              to="/"
              data-dismiss="modal"
              >Retour au site</nuxt-link
            >
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { jsPDF } from "jspdf"
export default {
  head() {
    return {
      meta: [
        {
          name: "description",
          content:
            "Formulaire d'inscription aux stange de danse organisé par l'association Images et Mouvements",
        },
      ],
    }
  },
  data() {
    return {
      mail: "",
      stageName: "",
      startDate: "",
      endDate: "",
      childName: "",
      childBirthDate: null,
      bloodGroup: "",
      childSpecialEat: "",
      parentName: "",
      parentName2: "",
      adress: "",
      zip: "",
      city: "",
      phoneNumber: "",
      email: "",
      mobileNumber: "",
      mobileNumber2: "",
    }
  },
  created() {
    this.stageName = this.$route.query.stageName
    this.startDate = this.$route.query.startDate
    this.endDate = this.$route.query.endDate
    this.mail =
      "mailto:asso.imagesetmouvements@gmail.com?Inscription%20stage%20du%20" +
      this.startDate
  },
  methods: {
    convertDate(d) {
      if (d == undefined || d == null) {
        return "    /    /    "
      } else {
        const date = new Date(d)
        const year = date.getFullYear()
        const month = date.getMonth() + 1
        const day = date.getDate()
        return day + "/" + month + "/" + year
      }
    },
    createPdf() {
      const doc = new jsPDF()
      doc.setFontSize(26)
      doc.text("Association Images et Mouvements", 30, 20)
      doc.setFontSize(22)
      doc.text("Formulaire d'inscription", 60, 35)
      doc.setFontSize(16)
      doc.text(this.stageName, 15, 50)
      doc.setFontSize(14)
      doc.text(
        "Du " +
          this.convertDate(this.startDate) +
          " au " +
          this.convertDate(this.endDate),
        15,
        60
      )
      doc.setFontSize(14)
      doc.text("Nom et prénom de l'élève : " + this.childName, 15, 75)
      doc.setFontSize(14)
      doc.text(
        "Date de naissance de l'élève : " +
          this.convertDate(this.childBirthDate),
        15,
        85
      )
      doc.setFontSize(14)
      doc.text("Groupe sanguin de l'élève : " + this.bloodGroup, 15, 95)
      doc.setFontSize(14)
      doc.text(
        "Régime alimentaire particulier : " + this.childSpecialEat,
        15,
        105
      )
      doc.setFontSize(14)
      doc.text("Nom et prénom des parents : " + this.parentName, 15, 115)
      doc.setFontSize(14)
      doc.text(this.parentName2, 81, 125)
      doc.setFontSize(14)
      doc.text("Adresse postale : " + this.adress, 15, 135)
      doc.setFontSize(14)
      doc.text(this.zip + " " + this.city, 55, 145)
      doc.setFontSize(14)
      doc.text("N° de téléphone des parents : " + this.phoneNumber, 15, 155)
      doc.setFontSize(14)
      doc.text("Email des parents : " + this.email, 15, 165)
      doc.setFontSize(14)
      doc.text(
        "N° de portable des parents à prevenir en cas d'urgence : " +
          this.mobileNumber,
        15,
        175
      )
      doc.setFontSize(14)
      doc.text(this.mobileNumber2, 141, 185)
      doc.setFontSize(14)
      doc.text("Fait à :", 125, 205)
      doc.setFontSize(14)
      doc.text("Le :", 125, 215)
      doc.setFontSize(14)
      doc.text("Signature des parents", 15, 235)
      doc.addPage("a4", "Autorisation parentale")
      doc.setFontSize(26)
      doc.text("Association Images et Mouvements", 30, 20)
      doc.setFontSize(22)
      doc.text("Autorisation parentale", 60, 35)
      doc.setFontSize(14)
      doc.text("Je soussigné " + this.parentName, 15, 50)
      doc.setFontSize(14)
      doc.text(
        [
          "Autorise l’association Images et Mouvements, par l’intermédiaire de Monsieur",
          "Henri Charbonnier, de Madame Monique Chevrier, ou tout autre adulte désigné",
          "par l’association, à véhiculer mon fils / ma fille durant les stages de Fretoy.",
        ],
        15,
        65
      )
      doc.setFontSize(14)
      doc.text(
        [
          "Cette autorisation comprend les trajets en voiture ou en bus (ligne régulière)",
          "de Nevers à Fretoy aller et retour, ainsi que les trajets entre Fretoy et",
          "Château-Chinon durant les semaines de stage.",
        ],
        15,
        90
      )
      doc.setFontSize(14)
      doc.text(
        "Fait à                                           , le     /    /                pour valoir ce que de droit",

        15,
        115
      )
      doc.setFontSize(14)
      doc.text(
        "Signature parentale",

        15,
        155
      )
      doc.save("formulaire-stage.pdf")
    },
  },
}
</script>

<style lang="scss" scoped>
.spacer {
  height: 150px;
}
.formInscription-title {
  color: $primaryDark;
}
.btn {
  background-color: $primaryDark;
}
@media (min-width: 992px) {
  .spacer {
    height: 50px;
  }
}
</style>
