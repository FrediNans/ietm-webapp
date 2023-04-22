<template>
  <div>
    <div class="col-4 m-4 d-flex">
      <button
        type="button"
        class="btn btn-primary"
        data-toggle="modal"
        data-target="#createStageModal"
        @click=";(isCreateModal = true) & (isModifyModal = false)"
      >
        + Ajouter un stage
      </button>
    </div>

    <div class="bg-light p-3">
      <h2 class="h4">Stage(s) obsolète(s)</h2>
      <div class="d-flex flex-row">
        <div
          v-for="passedStage in passedStages"
          :key="passedStage.id"
          class="d-flex flex-column"
        >
          <div
            class="d-flex flex-column p-4 m-3 border rounded bg-white shadow"
          >
            <div class="h6 text-center">{{ passedStage.name }}</div>
            <div>
              Du {{ convertDate(passedStage.startDate) }} au
              {{ convertDate(passedStage.endDate) }}
            </div>
          </div>
          <div class="col-6 mx-auto">
            <button
              class="btn btn-danger"
              @click="deletePassedStage(passedStage.id)"
            >
              Supprimer
            </button>
          </div>
        </div>
      </div>
    </div>

    <div class="bg-light p-3">
      <h2 class="h4">Stage(s) programmé(s)</h2>
      <div class="d-flex flex-row">
        <div
          v-for="programmedStage in programmedStages"
          :key="programmedStage.id"
          class="d-flex flex-column"
        >
          <div
            class="d-flex flex-column p-4 m-3 border rounded bg-white shadow"
          >
            <div class="h6 text-center">{{ programmedStage.name }}</div>
            <div>
              Du {{ convertDate(programmedStage.startDate) }} au
              {{ convertDate(programmedStage.endDate) }}
            </div>
          </div>
          <div class="d-flex justify-content-around">
            <button
              class="btn btn-danger"
              @click="deleteProgrammedStage(programmedStage.id)"
            >
              Supprimer
            </button>
            <button
              type="button"
              class="btn btn-warning"
              data-toggle="modal"
              data-target="#createStageModal"
              @click="
                ;(isCreateModal = false) & (isModifyModal = true),
                  getCurrentStage(programmedStage.id)
              "
            >
              Modifier
            </button>
          </div>
        </div>
      </div>
    </div>
    <!-- STAGE MODAL-->
    <div
      class="modal fade"
      id="createStageModal"
      tabindex="-1"
      aria-labelledby="createStageModalLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog modal-dialog-scrollable">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="createStageModalLabel">
              Ajouter un stage
            </h5>
            <button
              type="button"
              class="close"
              data-dismiss="modal"
              aria-label="Close"
            >
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
          <div class="modal-body">
            <div class="d-flex flex-column">
              <div class="d-flex flex-column pb-3 col-12">
                <label for="currentName">Intitulé du stage</label>
                <input id="currentName" type="text" v-model="currentName" />
              </div>
              <div class="col-12 d-flex justify-content-between">
                <div class="d-flex flex-column pb-3">
                  <label for="currentStartDate">Date de début</label>
                  <input
                    id="currentStartDate"
                    type="date"
                    v-model="currentStartDate"
                  />
                </div>
                <div class="d-flex flex-column pb-3">
                  <label for="currentEndDate">Date de fin</label>
                  <input
                    id="currentEndDate"
                    type="date"
                    v-model="currentEndDate"
                  />
                </div>
              </div>

              <div class="form-group col-12">
                <label for="currentDescription">Description</label>
                <textarea
                  class="form-control"
                  id="currentDescription"
                  rows="3"
                  v-model="currentDescription"
                ></textarea>
              </div>
              <div class="d-flex flex-column pb-3 col-12">
                <label for="currentPlace">Lieux du stage</label>
                <input id="currentPlace" type="text" v-model="currentPlace" />
              </div>
              <div class="d-flex flex-column pb-3 col-12">
                <label for="currentFullPrice"
                  >Prix du stage pension complète</label
                >
                <div class="input-group">
                  <input
                    id="currentFullPrice"
                    type="number"
                    class="form-control"
                    v-model="currentFullPrice"
                  />
                  <div class="input-group-append">
                    <span class="input-group-text">€</span>
                  </div>
                </div>
              </div>
              <div class="d-flex flex-column pb-3 col-12">
                <label for="currentExternalPrice">Prix du stage externat</label>
                <div class="input-group">
                  <input
                    id="currentExternalPrice"
                    type="number"
                    class="form-control"
                    v-model="currentExternalPrice"
                  />
                  <div class="input-group-append">
                    <span class="input-group-text">€</span>
                  </div>
                </div>
              </div>
              <div class="d-flex flex-column pb-3 col-12">
                <label for="currentUnitPrice">Prix d'un cours à l'unité</label>
                <div class="input-group">
                  <input
                    id="currentUnitPrice"
                    type="number"
                    class="form-control"
                    v-model="currentUnitPrice"
                  />
                  <div class="input-group-append">
                    <span class="input-group-text">€</span>
                  </div>
                </div>
              </div>
              <div class="form-group col-10 danger">
                <label for="actuImage">Ajouter une brochure pdf</label>
                <input
                  type="file"
                  class="form-control-file"
                  id="actuImage"
                  @change="addPdf"
                />
              </div>
              <div id="progressBar" v-if="uploadProgress > 0">
                <div
                  v-if="uploadProgress > 0"
                  id="progress"
                  role="progressbar"
                  aria-valuenow="75"
                  aria-valuemin="0"
                  aria-valuemax="100"
                  :style="{ width: uploadProgress + '%' }"
                ></div>
              </div>
            </div>
          </div>
          <div class="modal-footer">
            <button
              type="button"
              class="btn btn-secondary"
              data-dismiss="modal"
              @click="resetCurrentStage()"
            >
              Annuler
            </button>
            <button
              v-if="isCreateModal"
              data-dismiss="modal"
              type="button"
              class="btn btn-primary"
              @click="addStage()"
            >
              Ajouter
            </button>
            <button
              v-if="isModifyModal"
              data-dismiss="modal"
              type="button"
              class="btn btn-primary"
              @click="modifyStage(currentId)"
            >
              Modifier
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { db, storage } from "~/plugins/firebase"

import {
  collection,
  getDocs,
  addDoc,
  doc,
  deleteDoc,
  setDoc,
} from "firebase/firestore"

import { ref, uploadBytesResumable, getDownloadURL } from "firebase/storage"
export default {
  data() {
    return {
      stages: [],
      passedStages: [],
      programmedStages: [],
      currentId: "",
      currentName: "",
      currentStartDate: "",
      currentEndDate: "",
      currentDescription: "",
      currentPlace: "",
      currentFullPrice: 0,
      currentExternalPrice: 0,
      currentUnitPrice: 0,
      currentPdfUrl: "",
      uploadProgress: 0,
      isCreateModal: false,
      isModifyModal: false,
    }
  },
  layout: "admin",
  beforeMount() {
    this.getStages()
    this.isAdmin()
  },
  methods: {
    isAdmin() {
      const isAdmin = sessionStorage.getItem("isAdmin")
      if (isAdmin != "true") {
        this.$router.push({
          path: "/adminlogin",
        })
      }
    },
    convertDate(d) {
      const date = new Date(d)
      const year = date.getFullYear()
      const month = date.getMonth() + 1
      const day = date.getDate()
      return day + "/" + month + "/" + year
    },
    findPassedStages() {
      if (this.passedStages.length > 0) {
        this.passedStages = []
      }
      for (const stage in this.stages) {
        if (Date.parse(this.stages[stage].endDate) < Date.now()) {
          this.passedStages.push(this.stages[stage])
        }
      }
    },
    findProgrammedStages() {
      if (this.programmedStages.length > 0) {
        this.programmedStages = []
      }
      for (const stage in this.stages) {
        if (Date.parse(this.stages[stage].startDate) > Date.now()) {
          this.programmedStages.push(this.stages[stage])
        }
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
          startDate: doc.data().startDate,
          endDate: doc.data().endDate,
          description: doc.data().description,
          place: doc.data().place,
          pdfUrl: doc.data().pdfUrl,
          fullPrice: doc.data().fullPrice,
          externalPrice: doc.data().externalPrice,
          unitPrice: doc.data().unitPrice,
        })
      })
      this.findPassedStages()
      this.findProgrammedStages()
    },
    getCurrentStage(id) {
      const index = this.stages.findIndex((p) => p.id === id)
      this.currentId = id
      this.currentName = this.stages[index].name
      this.currentStartDate = this.stages[index].startDate
      this.currentEndDate = this.stages[index].endDate
      this.currentDescription = this.stages[index].description
      this.currentPlace = this.stages[index].place
      this.currentPdfUrl = this.stages[index].pdfUrl
      this.currentFullPrice = this.stages[index].fullPrice
      this.currentExternalPrice = this.stages[index].externalPrice
      this.currentUnitPrice = this.stages[index].unitPrice
    },
    resetCurrentStage() {
      this.currentId = ""
      this.currentName = ""
      this.currentStartDate = ""
      this.currentEndDate = ""
      this.currentDescription = ""
      this.currentPlace = ""
      this.currentPdfUrl = ""
      this.currentFullPrice = 0
      this.currentExternalPrice = 0
      this.currentUnitPrice = 0
    },
    async addStage() {
      await addDoc(collection(db, "stages"), {
        name: this.currentName,
        startDate: this.currentStartDate,
        endDate: this.currentEndDate,
        description: this.currentDescription,
        place: this.currentPlace,
        pdfUrl: this.currentPdfUrl,
        fullPrice: this.currentFullPrice,
        externalPrice: this.currentExternalPrice,
        unitPrice: this.currentUnitPrice,
      })
      this.getStages()
      this.resetCurrentStage()
    },
    async deletePassedStage(id) {
      const index = this.passedStages.findIndex((p) => p.id === id)
      await deleteDoc(doc(db, "stages", id))
      this.passedStages.splice(index, 1)
    },
    async deleteProgrammedStage(id) {
      const index = this.programmedStages.findIndex((p) => p.id === id)
      await deleteDoc(doc(db, "stages", id))
      this.programmedStages.splice(index, 1)
    },
    async modifyStage(id) {
      await setDoc(doc(db, "stages", id), {
        name: this.currentName,
        startDate: this.currentStartDate,
        endDate: this.currentEndDate,
        description: this.currentDescription,
        place: this.currentPlace,
        pdfUrl: this.currentPdfUrl,
        fullPrice: this.currentFullPrice,
        externalPrice: this.currentExternalPrice,
        unitPrice: this.currentUnitPrice,
      })
      this.resetCurrentStage()
      this.getStages()
    },
    addPdf(event) {
      const storageRef = ref(storage, "stages/" + event.target.files[0].name)
      const file = event.target.files[0]
      const uploadTask = uploadBytesResumable(storageRef, file)
      uploadTask.on(
        "state_changed",
        (snapshot) => {
          const progress =
            (snapshot.bytesTransferred / snapshot.totalBytes) * 100
          this.uploadProgress = progress

          switch (snapshot.state) {
            case "paused":
              console.log("Upload is paused")
              break
            case "running":
              console.log("Upload is running")
              break
          }
        },
        (error) => {
          console.log(error)
        },
        () => {
          getDownloadURL(uploadTask.snapshot.ref).then((downloadURL) => {
            console.log(downloadURL)
            this.currentPdfUrl = downloadURL
            this.uploadProgress = 0
          })
        }
      )
    },
  },
}
</script>

<style lang="scss" scoped></style>
