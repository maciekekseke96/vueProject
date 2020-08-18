<template>
  <div class="userDataForm">
    <div class="mainSection">
      <h1>Dane potrzebne do zamówienia</h1>
      <div class="forms">
        <form>
          <h2>Dane podstawowe</h2>
          <label>Imię *</label>
          <input
            class="required"
            type="text"
            placeholder="Imię"
            v-model="userData.name"
          />
          <label>Nazwisko *</label>
          <input
            class="required"
            type="text"
            placeholder="Nazwisko"
            v-model="userData.surname"
          />
          <label>Telefon</label>
          <input
            type="text"
            placeholder="Telefon"
            v-model="userData.telephone"
          />
          <label>Adres E-mail *</label>
          <input
            class="required"
            type="email"
            placeholder="e-mail"
            v-model="userData.email"
          />
        </form>
        <form>
          <h2>Dane adresowe</h2>
          <label>Ulica *</label>
          <input
            class="required"
            type="text"
            placeholder="Ulica"
            v-model="userData.street"
          />
          <label>Numer budynku *</label>
          <input
            class="required"
            type="text"
            placeholder="Numer budynku"
            v-model="userData.building"
          />
          <label>Numer mieszkania</label>
          <input
            type="text"
            placeholder="Numer mieszkania"
            v-model="userData.flat"
          />
          <label>Kod pocztowy *</label>
          <input
            class="required"
            type="text"
            placeholder="Kod pocztowy"
            v-model="userData.postalCode"
          />
          <label>Miasto *</label>
          <input
            class="required"
            type="text"
            placeholder="Miasto"
            v-model="userData.city"
          />
        </form>
      </div>
      <div class="controlButtons">
        <div class="btn" v-on:click="sendDataToApp(2)">
          Wstecz
        </div>
        <div class="btn" v-on:click="checkForm">
          Podsumowanie
        </div>
      </div>
      <div class="errors" v-if="mainErrors.length > 0">
        {{ mainErrors.join(", ") }} are required fields. Please check your data
      </div>
    </div>
    <overview
      v-bind:imageID="imageID"
      v-bind:printPlaces="printPlaces"
      v-bind:currentPrice="currentPrice"
    ></overview>
  </div>
</template>

<script>
import overview from "../Overview/overview.vue";

export default {
  props: {
    imageID: {
      type: Number,
    },
    currentPrice: {
      type: Number,
    },
    printPlaces: {
      type: Array,
    },
  },
  name: "userDataForm",
  components: {
    overview: overview,
  },
  data() {
    return {
      userData: {
        name: "",
        surname: "",
        telephone: "",
        email: "",
        street: "",
        building: "",
        flat: "",
        postalCode: "",
        city: "",
      },
      mainErrors: [],
    };
  },
  methods: {
    changeAppControler: function (controler) {
      this.$emit(`changeAppControler`, controler);
    },
    sendDataToApp: function (controler) {
      this.$emit(`dataSentfromUserForm`, {
        userData: this.userData,
      });
      this.changeAppControler(controler);
    },
    checkForm: function () {
      this.mainErrors = [];
      let required = [
        "name",
        "surname",
        "email",
        "street",
        "building",
        "postalCode",
        "city",
      ];
      required.forEach((field) => {
        if (this.userData[field].length < 1) {
          this.mainErrors.push(field);
        }
      });
      console.log(this.mainErrors);
      if (this.mainErrors.length < 1) {
        this.sendDataToApp(4);
      }
    },
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Russo+One&display=swap");

.userDataForm {
  width: 80vw;
  height: 70vh;
  border: 4px solid black;
  margin: 40px auto;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #2b7a78;
}

.mainSection {
  height: 100%;
  width: 70%;
  border-right: 2px solid black;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 30px;
  position: relative;
}
.mainSection h1 {
  font-family: "Russo One", sans-serif;
  color: #def2f1;
}

label,
input {
  display: block;
  font-family: "Russo One", sans-serif;
  color: #def2f1;
  font-size: 19px;
}

input {
  margin-bottom: 25px;
  color: #17252a;
  font-family: "Russo One", sans-serif;
}
form {
  margin: 30px;
  padding: 15px;
  border: 1px solid black;
}

form h2 {
  font-family: "Russo One", sans-serif;
  color: #17252a;
  margin-bottom: 20px;
}
label {
  font-family: "Russo One", sans-serif;
  color: #def2f1;
  margin-bottom: 10px;
}

.forms {
  display: flex;
}
.controlButtons {
  width: 70%;
  height: 40px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.btn {
  height: 100%;
  width: 30%;
  border: 1px solid black;
  font-family: "Russo One", sans-serif;
  font-size: 20px;
  color: #def2f1;
  background-color: #17252a;
  display: flex;
  justify-content: center;
  align-items: center;
  text-transform: uppercase;
}

.btn:hover {
  cursor: pointer;
  transform: scale(1.08);
}
.errors {
  width: 100%;
  border: 2px solid black;
  display: flex;
  flex-direction: column;
  align-items: center;
  font-family: "Russo One", sans-serif;
  color: red;
  font-size: 25px;
  position: absolute;
  left: 0;
  bottom: -120px;
  background-color: #def2f1;
}
</style>
