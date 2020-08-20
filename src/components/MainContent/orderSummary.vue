<template>
  <div class="orderSummary">
    <div class="mainSection">
      <h1 v-on:click="handle">Podsumowanie Twojego zamówienia</h1>
      <div class="mainSummary">
        <p><span class="upper">Nadruk</span>
        <p>
          Miejsce nadruku:
          <span v-if="printPlaces.includes('front')" class="mainData">Przód </span>
          <span v-if="printPlaces.length === 2" class="mainData">i </span>
          <span v-if="printPlaces.includes('back')" class="mainData">Tył</span>
          </p>
        </p>
        <p><span class="upper">Dane do wysyłki</span>
        <ul>
        <li>Imię: <span class="mainData">{{userData.imie}}</span> Nazwisko: <span class="mainData">{{userData.nazwisko}}</span></li>
        <li>Email: <span class="mainData">{{userData.email}}</span> <span v-if="userData.telefon.length===9">Telefon: <span class="mainData">{{userData.telefon}}</span></span></li>
        <li>Ulica: <span class="mainData"> {{userData.ulica}}</span> Numer domu: <span class="mainData">{{userData.numerDomu}}</span> <span v-if="userData.numerMieszkania.length>0">Numer mieszkania: <span class="mainData">{{userData.numerMieszkania}}</span></span></li>
        <li>Kod Pocztowy: <span class="mainData">{{userData.kodPocztowy}}</span> Miasto: <span class="mainData">{{userData.miasto}}</span></li>
        </ul>
        </p>
        <p class="upper">Potwierdzenie sekcji zamówienia</p>
        <div class="confirmingSection">
          <div class="confirm">
            <h5>Miejsce druku</h5>
            <div class="confirmBtn" v-on:click="confirmPrintPlace">Potwierdź</div>
            <div class="editBtn" v-on:click="editChooseImage">Edytuj</div>
          </div>
          <div class="confirm">
                      <h5>Obrazek</h5>
            <div class="confirmBtn" v-on:click="confirmChooseImage">Potwierdź</div>
            <div class="editBtn" v-on:click="editChooseImage">Edytuj</div>
          </div>
          <div class="confirm">
                      <h5>Dane klienta</h5>
            <div class="confirmBtn" v-on:click="confirmUserForm">Potwierdź</div>
            <div class="editBtn" v-on:click="editUserForm">Edytuj</div></div>
        </div>
      </div>
      <div class="controlButtons">
        <div class="btn" v-on:click="sendDataToApp(3)">
          Wstecz
        </div>
        <div class="btn" v-on:click="finalize">
          Zamów
        </div>
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
    userData: {
      type: Object,
    },
  },
  name: "orderSummary",
  components: {
    overview: overview,
  },
  data() {
    return {
      confirmed: [],
    };
  },
  watch: {
    userData: function (newData) {
      this.userData = newData;
    },
  },
  methods: {
    handle: function () {
      console.log(this.userData);
    },
    changeAppControler: function (controler) {
      this.$emit(`changeAppControler`, controler);
    },
    sendDataToApp: function (controler) {
      this.changeAppControler(controler);
    },
    confirmPrintPlace: function(event){
        this.confirmed.push("printPlace");
        event.target.parentElement.style.backgroundColor = "green";
    },
    confirmChooseImage: function(event){
        this.confirmed.push("chooseImage");
        event.target.parentElement.style.backgroundColor = "green";
    } ,   
    confirmUserForm: function(event){
        this.confirmed.push("userForm");
        event.target.parentElement.style.backgroundColor = "green";
    } ,   
    editPrintPlace: function(event){
        event.target.parentElement.style.backgroundColor = "#2b7a78";
        let confirmed = this.confirmed.filter(element => element!=="printPlace");
        this.confirmed = confirmed;
        this.changeAppControler(1);
    },
    editChooseImage: function(event){
        event.target.parentElement.style.backgroundColor = "#2b7a78";
        let confirmed = this.confirmed.filter(element => element!=="chooseImage");
        this.confirmed = confirmed;
        this.changeAppControler(2);
    },
    editUserForm: function(event){
        event.target.parentElement.style.backgroundColor = "#2b7a78";
        let confirmed = this.confirmed.filter(element => element!=="userForm");
        this.confirmed = confirmed;
        this.changeAppControler(3);
    },
    finalize: function(){
      if(this.confirmed.length===3){
        let summaryObject = {
          image: {
            loremId: this.imageID,
            printPlaces: this.printPlaces,
          },
          userData: {
            name: this.userData.imie,
            surname: this.userData.nazwisko,
            telephone: this.userData.telefon,
            email: this.userData.email,
            address: {
              street: this.userData.ulica,
              home: this.userData.numerDomu,
              flat: this.userData.numerMieszkania,
              postalCode: this.userData.kodPocztowy,
              city: this.userData.miasto,
            }
          },
          price: this.currentPrice,
        };
        this.changeAppControler(5);
        console.log(summaryObject);
        return summaryObject;
      }else{
        alert("Musisz potwierdzić wszystkie sekcje przed złożeniem zamówienia");
      }  
    }
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Russo+One&display=swap");

.orderSummary {
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
}
.mainSection h1 {
  font-family: "Russo One", sans-serif;
  color: #def2f1;
}
 h5{
     font-family: "Russo One", sans-serif;
  color: #def2f1;
 }

.mainSummary {
  width: 90%;
  height: 75%;
  margin-top: 40px;
  border: 1px solid black;
  padding: 10px;
}

.controlButtons {
  width: 100%;
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

.mainData {
  color: #17252a;
  margin-right: 15px;
}

.btn:hover {
  cursor: pointer;
  transform: scale(1.08);
}

p {
  color: #def2f1;
  font-family: "Russo One", sans-serif;
  margin-bottom: 10px;
  margin-top: 10px;
}
ul {
  margin-bottom: 30px;
  margin-top: 10px;
}

ul {
  list-style-type: none;
}
.upper {
  text-transform: uppercase;
  font-size: 20px;
}

.confirmingSection {
  width: 100%;
  height: 20%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 40px;
}

.confirm {
  width: 20%;
  height: 100%;
  border: 1px solid black;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  color: #17252a;
  background-color: none;
}

.confirmBtn, .editBtn {
  width: 100%;
  height: 20%;
  background-color: #17252a;
  color: #def2f1;
  font-family: "Russo One", sans-serif;
  display: flex;
  justify-content:center;
  align-items: center;

}
.confirmBtn:hover, .editBtn:hover {
transform: scale(1.05);
cursor: pointer;
}
</style>
