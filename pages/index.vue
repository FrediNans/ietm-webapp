<template>
  <div class="">
    <!-- SECTION BANDEAU TOP -->

    <div class="" id="img-box">
      <img
        id="img-top"
        src="../static/images/cloture.jpg"
        alt="Festival traverses slaves à Château-Chinon"
      />
      <div id="img-text" class="p-2 col-10">
        <h2 class="text-center text-white h5">
          Bienvenue sur le site de l’association Images et Mouvements !
        </h2>
      </div>
    </div>
    <!-- SECTION PRESENTATION -->

    <section class="presentation d-md-flex col-12">
      <div
        class="presentation__img d-flex justify-content-center align-items-center"
      >
        <div class="presentation__img__box">
          <img
            class="presentation__img__box__img"
            src="../static/images/stage.jpg"
            alt="Stagiare de l'association Images et Mouvements"
          />
        </div>
        <div class="presentation__img__deco"></div>
      </div>
      <div
        class="presentation__text px-3 d-md-flex flex-column justify-content-center px-md-5"
      >
        <h1 class="h3">PRÉSENTATION</h1>
        <p class="text-justify">
          L’association à but non lucratif Images et Mouvements est une instance
          Morvandelle dont le Siège Social est situé au 21 rue des Fossés à
          Château-Chinon, déclarée à la sous-préfecture de Château -Chinon.<br />
          Depuis avril 2016, l’association a pour mission de soutenir la culture
          en milieu rural.<br />
          L’association agit dans quatre champs que sont la création, la
          diffusion, l’enseignement et l’action culturelle.
        </p>
      </div>
    </section>
    <!-- SECTION ACTU -->
    <section class="p-0 actu col-12 pb-lg-5">
      <h1 class="h3 text-center pt-3 actu__title">ACTUALITÉ</h1>
      <div
        class="actu__navbox h5 d-flex justify-content-between align-items-center col-md-8 col-lg-6 mx-auto pb-1"
      >
        <button @click="getActuByIndex(actusIndex - 1)" class="actu__btn">
          <span class="material-icons-outlined"> arrow_circle_left </span>
        </button>
        <div>
          {{ actusIndex + 1 + "/" + actus.length }}
        </div>
        <button @click="getActuByIndex(actusIndex + 1)" class="actu__btn">
          <span class="material-icons-outlined"> arrow_circle_right </span>
        </button>
      </div>
      <div class="bg-light col-12 col-lg-8 mx-lg-auto p-3 rounded">
        <h2 class="h4 text-center actu__title2">{{ currentActu.title }}</h2>
        <div
          class="d-flex flex-column flex-md-row align-items-center justify-content-md-around"
        >
          <img
            :src="currentActu.imgUrl"
            v-if="currentActu.imgUrl != null"
            class="actu__img p-0 pb-3 col-md-6"
          />
          <p class="text-justify col-md-6 p-0 pl-md-3">
            {{ currentActu.intro }}
          </p>
        </div>
        <p class="text-justify">{{ currentActu.text1 }}</p>
        <p class="text-justify">{{ currentActu.text2 }}</p>
      </div>
    </section>
    <section class="coming p-0 col-12 bg-secondary pb-md-3">
      <h1 class="coming__title h3 text-center py-3 pt-lg-4 mb-lg-3">A VENIR</h1>
      <div
        class="d-flex flex-column align-items-center flex-lg-row justify-content-lg-around"
      >
        <div
          @click="goTo('festival')"
          class="coming__thumbnail p-0 d-flex flex-column align-items-center bg-white col-10 mb-3 flex-md-row col-md-7 col-lg-4"
        >
          <img
            class="coming__thumbnail-img mb-3 p-0 mb-md-0 col-md-6 p-md-0"
            src="../static/images/festival/festival-1.webp"
            alt="Festival traverses, chanteur et pianiste à château-chinon dans la Nièvre"
          />
          <div class="col-md-6 d-flex flex-column align-items-center p-0">
            <h2 class="h4 coming__thumbnail-title">Festival</h2>
            <h3 class="h5 coming__thumbnail-title">{{ festival.title }}</h3>
            <p>
              Du <span>{{ convertDate(festival.startDate) }}</span> au
              <span>{{ convertDate(festival.endDate) }}</span>
            </p>
          </div>
        </div>
        <div
          @click="goTo('stages')"
          class="coming__thumbnail p-0 d-flex flex-column align-items-center bg-white col-10 mb-3 flex-md-row col-md-7 col-lg-4"
        >
          <img
            class="coming__thumbnail-img mb-3 p-0 mb-md-0 col-md-6 p-md-0"
            src="../static/images/stage/stage-4.webp"
            alt="Jeunes danseurs stagiaire de l'association images et mouvements"
          />
          <div class="col-md-6 d-flex flex-column align-items-center p-0">
            <h2 class="h4 coming__thumbnail-title">
              {{ firstValidStage.name }}
            </h2>
            <p>
              Du <span>{{ convertDate(firstValidStage.startDate) }}</span> au
              <span>{{ convertDate(firstValidStage.endDate) }}</span>
            </p>
          </div>
        </div>
      </div>
    </section>
    <div class="partner p-3 d-flex flex-column">
      <h1 class="partner__title h3 text-center py-3">PARTENAIRES</h1>

      <div class="d-flex flex-wrap justify-content-around">
        <div class="col-6 col-md-4 col-lg-2 mb-3">
          <img
            src="../static/images/logos/logo-ville.png"
            class="img-fluid"
            alt="Logo ville de Château Chinon"
          />
        </div>
        <div class="col-6 col-md-4 col-lg-2 mb-3">
          <img
            src="../static/images/logos/logo-comcom.png"
            class="img-fluid"
            alt="Logo comunauté de commune du Morvan"
          />
        </div>
        <div class="col-6 col-md-4 col-lg-2 mb-3">
          <img
            src="../static/images/logos/logo-minist.png"
            class="img-fluid"
            alt="Logo ministère de l'éducation nationale"
          />
        </div>
        <div class="col-6 col-md-4 col-lg-2 mb-3">
          <img
            src="../static/images/logos/logo-cdn.png"
            class="img-fluid"
            alt="Logo conseil départementale de la nièvre"
          />
        </div>
        <div class="col-6 col-md-4 col-lg-2 mb-3">
          <img
            src="../static/images/logos/logo-cacl.png"
            class="img-fluid"
            alt="Logo crédit agricole Centre Loire"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { db } from "~/plugins/firebase"
import { collection, getDocs } from "firebase/firestore"
export default {
  head() {
    return {
      meta: [
        {
          name: "description",
          content:
            "L’association à but non lucratif Images et Mouvements est une instance Morvandelle dont le Siège Social est situé au 21 rue des Fossés à Château-Chinon, déclarée à la sous-préfecture de Château-Chinon. Depuis avril 2016, l’association a pour mission de soutenir la culture en milieu rural. L’association agit dans quatre champs que sont la création, la diffusion, l’enseignement et l’action culturelle.",
        },
      ],
    }
  },
  data() {
    return {
      actus: [],
      actusIndex: 0,
      currentActu: {},
      stages: [],
      validStages: [],
      firstValidStage: {},
      festival: {
        title: "Traverses Slaves",
        startDate: "2023-07-13",
        endDate: "2023-07-28",
      },
      currentLogoUrl: "",
      logoUrl: [
        "../images/logos/log-ville.jpg",
        "../images/logos/logo-comcom.png",
      ],
    }
  },
  beforeMount() {
    this.getActus()
    this.getStages()
  },

  methods: {
    changeLogo() {},
    goTo(r) {
      this.$router.push("/" + r)
    },
    convertDate(d) {
      const date = new Date(d)
      const year = date.getFullYear()
      const month = date.getMonth() + 1
      const day = date.getDate()
      return day + "/" + month + "/" + year
    },
    async getActus() {
      if (this.actus.length > 0) {
        this.actus = []
      }
      const querySnapshot = await getDocs(collection(db, "actus"))
      querySnapshot.forEach((doc) => {
        this.actus.push({
          id: doc.id,
          title: doc.data().title,
          intro: doc.data().intro,
          text1: doc.data().text1,
          text2: doc.data().text2,
          imgUrl: doc.data().imgUrl,
          imgName: doc.data().imgName,
        })
      })
      this.getActuByIndex(this.actusIndex)
    },
    getActuByIndex(index) {
      if (index > this.actus.length - 1 || index < 0) {
        return
      }
      this.actusIndex = index
      this.currentActu = {
        title: this.actus[index].title,
        intro: this.actus[index].intro,
        text1: this.actus[index].text1,
        text2: this.actus[index].text2,
        imgUrl: this.actus[index].imgUrl,
      }
    },
    findValidStages() {
      if (this.validStages.length > 0) {
        this.validStages = []
      }
      for (const stage in this.stages) {
        if (Date.parse(this.stages[stage].startDate) > Date.now()) {
          this.validStages.push(this.stages[stage])
        }
      }
      const stagesSorted = this.validStages.sort((a, b) => {
        a = a.startDate
        b = b.startDate
        return a > b ? -1 : a < b ? 1 : 0
      })
      stagesSorted.reverse()
      this.firstValidStage = {
        name: stagesSorted[0].name,
        startDate: stagesSorted[0].startDate,
        endDate: stagesSorted[0].endDate,
      }
    },
    async getStages() {
      if (this.stages.length > 0) {
        this.stages = []
      }
      const querySnapshot = await getDocs(collection(db, "stages"))
      querySnapshot.forEach((doc) => {
        this.stages.push({
          id: doc.id,
          name: doc.data().name,
          startDate: new Date(doc.data().startDate),
          endDate: new Date(doc.data().endDate),
        })
      })
      this.findValidStages()
    },
  },
}
</script>

<style lang="scss" scoped>
h1,
h2 {
  color: $primary;
}
#img-box {
  position: relative;
}
#img-top {
  height: 400px;
  width: 100%;
  object-fit: cover;
}
#img-text {
  position: absolute;
  background-color: rgba($color: #000000, $alpha: 0.6);
  top: 80%;
  left: 50%;
  transform: translateX(-50%);
  border-radius: 10px;
}
.presentation {
  &__img {
    height: 500px;
    width: 100%;
    &__box {
      border: 5px solid white;
      width: 320px;
      height: 320px;
      border-radius: 50%;
      overflow: hidden;
      &__img {
        object-fit: cover;
        width: 320px;
        height: 320px;
      }
    }
    &__deco {
      position: absolute;
      z-index: -1;
      margin-left: 10px;
      margin-top: 20px;
      width: 320px;
      height: 320px;
      border-radius: 50%;
      background-color: $primary;
    }
  }
}
.actu {
  background-color: $primaryDark;
  &__navbox {
    color: white;
  }
  &__title {
    color: white;
  }
  &__title2 {
    color: $primaryDark;
  }
  &__btn {
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: $primaryDark;

    color: white;
    border: none;
    border-radius: 50%;
    cursor: pointer;
    width: 45px;
    height: 45px;
    margin: 0;
    padding: 0;
    &:hover {
      background-color: $primaryLight;
    }
  }
  &__imgBox {
    width: 150px;
    height: 150px;
  }
  &__img {
    height: 250px;
    width: 300px;
    object-fit: cover;
  }
}
.coming {
  &__title {
    color: $primaryLight;
  }
  &__thumbnail {
    border-radius: 10px;
    overflow: hidden;
    color: #000000;
    cursor: pointer;
    text-decoration: none;
  }
  &__thumbnail-img {
    width: 100%;
    height: 200px;
    object-fit: cover;
  }
  &__thumbnail-title {
    color: $primaryDark;
  }
}
.partner {
  &__title {
    color: $secondary;
  }
}
</style>
