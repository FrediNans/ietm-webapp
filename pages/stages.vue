<template>
  <div>
    <PageBaner
      pageTitle="STAGES"
      pageTitle2=""
      imgUrl="../images/stage/stage-11.webp"
      imgTextAlt="Stage 2020, cours de réveil corporel, conduit par Henri Charbonnier."
    />
    <div class="spacer"></div>
    <div class="p-3 col-md-10 col-lg-8 col-xl-6 mx-md-auto">
      <h1 class="h3 text-center stage-title mb-4">Stage de danse pluridisciplinaires</h1>
      <p class="text-justify">
        L’association Images et Mouvements organise lors des vacances scolaires, des stages de danse pluridisciplinaires. La coordination pédagogique est assurée par Henri Charbonnier, entouré d’une équipe diplômée et reconnue par le Ministère de la Culture et de la Communication :
      </p>
      <p class="text-justify">
        <strong>Pascale Jullien</strong> de l’Opéra de Zurich ( Danse Classique ), <strong>Roxana Barbacaru</strong> de l’Opéra National de Paris ( Danse de Caractère ), <strong>Marie Laure Agrapart</strong> de la compagnie Rambert à Londres ( Danse Contemporaine ), <strong>Alberto Morino</strong> du Ballet de l’Opéra National de Finlande ( Danse Classique ), <strong>Alice Psaroudaki</strong> de l’Opéra de Berlin ( Répertoire ), <strong>Cécile Berrebi de Noailles</strong> de la compagnie Pina Bausch ( Danse Contemporaine ), <strong>Serge Ambert</strong> de l’Opéra de Lyon ( Atelier Contemporain ), <strong>Henri Charbonnier</strong> des Ballets de Monte Carlo ( Eveil Corporel ), <strong>Mireille Letterier</strong> du Pittsburgh Ballet ( Danse Classique ).
      </p>
      <p class="text-justify">
        L’association limite le nombre d’inscriptions aux stages afin de soigner particulièrement le suivi pédagogique des élèves, leur évolution au cours de la semaine, dans une approche personnalisée. Il leur est proposé une scène tremplin tous les deux ans lors du stage d’été dans le cadre du festival « Traverses, événement artistique ».
      </p>
      <p class="text-justify">Le stage est ouvert en pension complète ou en externe et  propose 4 cours par jour en moyenne (environ 30 heures de cours sur la semaine). Le stage accueille également des publics diversifiés, amateurs, adultes, et élèves qui se destinent à une carrière professionnelle. Dans ce cadre, les cours peuvent être dédoublés en fonction des niveaux.</p>
    </div>
    <div
      class="p-3 col-md-10 mx-md-auto col-lg-10 "
    >
    <hr class="mb-lg-5">
      <div
        v-for="validStage in validStages"
        :key="validStage.id"
        class="d-lg-flex justify-content-lg-center p-lg-0 thumbnail "
      >
     
        <img
          :src="require(`../static/images/stage/stage-${Math.floor(Math.random() * 12) + 1}.webp`)"
          class="stage__img col-lg-4 p-lg-0"
          alt="Eleve d'un stage de danse organisé par l'association images et mouvements dans la Nièvre à Fretoy"
        />
        <div class="py-3 col-lg-8">
          <h2 class="h4 card-title text-center">{{ validStage.name }}</h2>

          <div class="text-center">
            Du {{ convertDate(validStage.startDate) }} au
            {{ convertDate(validStage.endDate) }}
          </div>
          <div class="text-justify my-2">
            {{ validStage.description }}
          </div>
          <div>
            Pension complète : {{ validStage.fullPrice }} €
          </div>
          <div>
            Externat : {{ validStage.externalPrice }} €
          </div>
          <div>
            Cours à l'unité : {{ validStage.unitPrice }} €
          </div>
          <div>
            <div class="py-2 text-justify">
            Tous les détails de ce stage sont disponible sur notre brochure.
            </div>
            <div class="text-center py-2">
            <a
            class="btn btn-info"
            :href="validStage.pdfUrl"
            target="blank"
            >
            Télécharger la brochure
          </a>
          <nuxt-link
            class="btn btn-success"
            :to="{
              path: 'stageInscription',
              query: {
                stageName: validStage.name,
                startDate: validStage.startDate,
                endDate: validStage.endDate,
              },
            }"
            >Inscription</nuxt-link
          >
          </div>
          </div>
        </div>
      </div>
      
    </div>
    <div
      v-if="currentIndex != null"
      class="modal fade"
      id="stageModal"
      tabindex="-1"
      aria-labelledby="createStageModalLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title">
              Stage {{ validStages[currentIndex].name }}
            </h5>
            <button
              @click="currentIndex = null"
              type="button"
              class="close"
              data-dismiss="modal"
              aria-label="Close"
            >
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
          <div class="modal-body">
            <p>
              Le stage se déroulera du
              {{ convertDate(validStages[currentIndex].startDate) }} au
              {{ convertDate(validStages[currentIndex].endDate) }} à
              {{ validStages[currentIndex].place }}.
            </p>
            <p>{{ validStages[currentIndex].description }}</p>
            <p>
              Le coût du stage est de {{ validStages[currentIndex].price }} €
            </p>
            <p>
              Professeurs présents lors du stage : <ul v-for="prof in validStages[currentIndex].animators" :key="prof">
                <li v-if="prof != null">{{ prof }}</li>
              </ul>
            </p>
          </div>
          <div class="modal-footer">
            <button
              type="button"
              class="btn btn-secondary"
              data-dismiss="modal"
              @click="currentIndex = null"
            >
              Retour
            </button>
           <nuxt-link
            class="btn btn-success"
            data-dismiss="modal"
            :to="{
              path: 'stageInscription',
              query: {
                stageName: validStages[currentIndex].name,
                startDate: validStages[currentIndex].startDate,
                endDate: validStages[currentIndex].endDate,
              },
            }"
            >Inscription</nuxt-link
          >
          </div>
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
            "L’association Images et Mouvements organise lors des vacances scolaires dans le Morvan, des stages de danse pluridisciplinaires. La coordination pédagogique est assurée par Henri Charbonnier, entouré d’une équipe diplômée et reconnue par le Ministère de la Culture et de la Communication",
        },
      ],
    }
  },
  data() {
    return {
      stages: [],
      validStages: [],
      currentIndex: null,
      textAlt: {
      },

    }
  },
  
  beforeMount() {
    this.getStages()
  },
  methods: {
    openModal() {
      $("#stageModal").modal("toggle")
    },
    convertDate(d) {
      const date = new Date(d)
      const year = date.getFullYear()
      const month = date.getMonth() + 1
      const day = date.getDate()
      return day + "/" + month + "/" + year
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
    },
    findStageById(id) {
      const index = this.stages.findIndex((p) => p.id === id)
      this.currentIndex = index
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
          startDate: doc.data().startDate,
          endDate: doc.data().endDate,
          description: doc.data().description,
          animators: doc.data().animators,
          place: doc.data().place,
          pdfUrl: doc.data().pdfUrl,
          fullPrice: doc.data().fullPrice,
          externalPrice: doc.data().externalPrice,
          unitPrice: doc.data().unitPrice,
        })
      })
      this.findValidStages()
    },
   
  },
}
</script>

<style lang="scss" scoped>
.spacer {
  height: 150px;
}
.stage-title {
  color: $primaryDark;
}

  .stage__img {
    
    object-fit: cover;
  }



@media (min-width: 992px) {
  .spacer {
    height: 50px;
  }
  .thumbnail {
  border: 1px solid rgb(194, 194, 194);
  border-radius: 10px;
  overflow: hidden;
  margin: 1rem 0 1rem 0;
}
}
</style>
