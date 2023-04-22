<template>
  <div>
    <h1 class="h3 text-center my-3">Connexion espace administrateur</h1>
    <div class="col-6 mx-auto">
      <div class="form-group">
        <label for="exampleInputEmail1">Email</label>
        <input
          type="email"
          class="form-control"
          id="exampleInputEmail1"
          v-model="adminEmail"
        />
      </div>
      <div class="form-group">
        <label for="exampleInputPassword1">Mot de passe</label>
        <input
          type="password"
          class="form-control"
          id="exampleInputPassword1"
          v-model="adminPassword"
        />
      </div>

      <button class="btn btn-primary" @click="adminLogin()">
        Se connecter
      </button>
    </div>
  </div>
</template>

<script>
import { getAuth, signInWithEmailAndPassword } from "firebase/auth"
export default {
  data() {
    return {
      adminEmail: "",
      adminPassword: "",
    }
  },
  layout: "admin",
  methods: {
    adminLogin() {
      const auth = getAuth()
      signInWithEmailAndPassword(auth, this.adminEmail, this.adminPassword)
        .then((userCredential) => {
          // Signed in
          const user = userCredential.user
          sessionStorage.setItem("isAdmin", true)
          this.$router.push({
            path: "/adminactus",
          })
        })
        .catch((error) => {
          const errorCode = error.code
          const errorMessage = error.message
          console.log(error)
        })
    },
  },
}
</script>
