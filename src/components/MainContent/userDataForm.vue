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
            v-model="userData.imie"
          />
          <label>Nazwisko *</label>
          <input
            class="required"
            type="text"
            placeholder="Nazwisko"
            v-model="userData.nazwisko"
          />
          <label class="specific"
            >Telefon
            <span
              v-if="specificErrors.includes('telefon')"
              class="errorPlaceholder"
              >Zła długość numeru</span
            ></label
          >
          <input
            type="text"
            placeholder="Telefon (123456789)"
            v-model="userData.telefon"
          />
          <label class="specific"
            >Adres E-mail *
            <span
              v-if="specificErrors.includes('email')"
              class="errorPlaceholder"
              >Sprawdz adres email</span
            ></label
          >
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
            v-model="userData.ulica"
          />
          <label>Numer budynku *</label>
          <input
            class="required"
            type="text"
            placeholder="Numer budynku"
            v-model="userData.numerDomu"
          />
          <label>Numer mieszkania</label>
          <input
            type="text"
            placeholder="Numer mieszkania"
            v-model="userData.numerMieszkania"
          />
          <label class="specific"
            >Kod pocztowy *
            <span
              v-if="specificErrors.includes('kodPocztowy')"
              class="errorPlaceholder"
              >Sprawdz kod pocztowy</span
            ></label
          >
          <input
            class="required"
            type="text"
            placeholder="Kod pocztowy (bez '-')"
            v-model="userData.kodPocztowy"
          />
          <label>Miasto *</label>
          <input
            class="required"
            type="text"
            placeholder="Miasto"
            v-model="userData.miasto"
          />
        </form>
        <div class="controlButtons">
          <div class="btn" v-on:click="sendDataToApp(2)">
            Wstecz
          </div>
          <div class="btn" v-on:click="checkForm">
            Podsumowanie
          </div>
        </div>
      </div>
      <div class="errors" v-if="mainErrors.length > 0">
        {{ mainErrors.join(", ") }} to dane wymagane. Uzupełnij je.
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
        imie: "",
        nazwisko: "",
        telefon: "",
        email: "",
        ulica: "",
        numerDomu: "",
        numerMieszkania: "",
        kodPocztowy: "",
        miasto: "",
      },
      mainErrors: [],
      specificErrors: [],
    };
  },
  methods: {
    changeAppControler: function (controler) {
      this.$emit(`changeAppControler`, controler);
    },
    sendDataToApp: function (controler) {
      this.$emit(`dataSentfromUserForm`, this.userData);
      this.changeAppControler(controler);
    },
    checkSpecificInputs: function () {
      this.specificErrors = [];
      if (!this.userData.email.includes("@")) {
        this.specificErrors.push("email");
      }
      if (
        this.userData.telefon.length != 9 &&
        this.userData.telefon.length != 0
      ) {
        this.specificErrors.push("telefon");
      }
      if (this.userData.kodPocztowy.length != 5) {
        this.specificErrors.push("kodPocztowy");
      }
    },
    checkForm: function () {
      this.mainErrors = [];
      let required = [
        "imie",
        "nazwisko",
        "email",
        "ulica",
        "numerDomu",
        "kodPocztowy",
      ];
      required.forEach((field) => {
        if (this.userData[field].length < 1) {
          this.mainErrors.push(field);
        }
      });
      this.checkSpecificInputs();
      if (this.mainErrors.length < 1 && this.specificErrors.length < 1) {
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
  position: relative;
}
.controlButtons {
  width: 100%;
  height: 40px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  position: absolute;
  bottom: 0;
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

.specific {
  position: relative;
}

.errorPlaceholder {
  position: absolute;
  color: red;
  bottom: -60px;
  left: 0;
}
</style>
