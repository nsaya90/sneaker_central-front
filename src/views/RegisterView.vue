<template lang="">
  <NavBar></NavBar>

  <div class="container-fluid">
    <p class="text-register">
      N'hésitez plus et rejoignez notre communauté de passionnés de sneakers
      pour trouver la paire parfaite ou vendre celle que vous ne portez plus.
    </p>
    <div class="d-flex justify-content-center">
      <div class="box-register">
        <form class="form_register" action="" @submit.prevent>
          <div class="form-floating mb-3">
            <input
              type="text"
              class="form-control"
              id="inputFirstname"
              placeholder="Nom"
              v-model="firstname"
            />
            <label for="inputFirstname">Nom</label>
            <p
              class="errors"
              v-if="this.errors.firstname"
              v-text="errors.firstname[0]"
            ></p>
          </div>
          <div class="form-floating mb-3">
            <input
              type="text"
              class="form-control"
              id="inputLastName"
              placeholder="Prénom"
              v-model="lastname"
            />
            <label for="inputLastName">Prénom</label>
            <p
              class="errors"
              v-if="this.errors.lastname"
              v-text="errors.lastname[0]"
            ></p>
          </div>
          <div class="form-floating mb-3">
            <input
              type="text"
              class="form-control"
              id="inputPhone"
              placeholder="Numéro de téléphone"
              v-model="phone"
            />
            <label for="inputPhone">Numéro de téléphone</label>
            <p
              class="errors"
              v-if="this.errors.phone"
              v-text="errors.phone[0]"
            ></p>
          </div>
          <div class="form-floating mb-3">
            <input
              type="email"
              class="form-control"
              id="inputEmail"
              placeholder="Email"
              v-model="email"
            />
            <label for="inputEmail">Email</label>
            <p class="errors" v-if="this.errorMail" v-text="errorMail"></p>
            <p
              class="errors"
              v-if="this.errors.email"
              v-text="errors.email[0]"
            ></p>
          </div>
          <div class="form-floating mb-3">
            <input
              type="password"
              class="form-control"
              id="inputPassword"
              placeholder="password"
              v-model="password"
            />
            <label for="inputPassword">Mot de passe</label>
            <p
              class="errors"
              v-if="this.errors.password"
              v-text="errors.password[0]"
            ></p>
          </div>
          <button class="button-23" @click="register" type="button">
            S'inscrire
          </button>
        </form>
      </div>
    </div>
    <div class="box-register-login">
      <p class="text-register">
        Déjà inscrit ? <router-link to="/login">Se connecter</router-link>
      </p>
    </div>
  </div>
</template>
<script>
import axios from "axios";
import NavBar from "@/components/NavBar.vue";

export default {
  name: "RegisterView",
  components: { NavBar },
  data() {
    return {
      infoUser: "",
      firstname: "",
      lastname: "",
      phone: "",
      email: "",
      password: "",
      errors: "",
      errorMail: "",
    };
  },

  methods: {
    async register() {
      await axios({
        method: "post",
        url: "http://127.0.0.1:8000/api/user",

        data: {
          firstname: this.firstname,
          lastname: this.lastname,
          phone: this.phone,
          email: this.email,
          password: this.password,
        },
      })
        .then((response) => (this.infoUser = response.data))
        .catch((error) => {
          this.errors = error.response.data.errors;
        });

      // this.$router.replace({ path: "/login" });
      // if (this.infoRegister) {
      //   location = "http://localhost:8080/login";
      // }
      if (this.infoRegister.error_mail) {
        this.errorMail = this.infoRegister.error_mail;
      }
    },
  },
};
</script>
<style scoped>
.box-register-login {
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;

  padding-top: 25px;
}

.box-register-login button {
  width: 60%;
}
.text-register {
  text-align: center;
}

form p {
  color: red;
}

.box-register {
  width: 100%;
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
}
.form_register {
  width: 60%;
}
.button-23 {
  background-color: #ffffff;
  border: 4px solid black;
  border-radius: 8px;
  box-sizing: border-box;
  color: #222222;
  cursor: pointer;
  display: inline-block;
  font-family: Circular, -apple-system, BlinkMacSystemFont, Roboto,
    "Helvetica Neue", sans-serif;
  font-size: 16px;
  font-weight: 600;
  line-height: 20px;
  height: 50px;
  margin: 0;
  outline: none;

  text-align: center;
  text-decoration: none;
  touch-action: manipulation;
  transition: box-shadow 0.2s, -ms-transform 0.1s, -webkit-transform 0.1s,
    transform 0.1s;
  user-select: none;
  -webkit-user-select: none;
  width: 100%;
}

.button-23:focus-visible {
  box-shadow: #222222 0 0 0 2px, rgba(255, 255, 255, 0.8) 0 0 0 4px;
  transition: box-shadow 0.2s;
}

.button-23:active {
  background-color: #f7f7f7;
  border-color: #000000;
  transform: scale(0.96);
}

.button-23:disabled {
  border-color: #dddddd;
  color: #dddddd;
  cursor: not-allowed;
  opacity: 1;
}
</style>
