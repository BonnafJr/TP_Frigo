<script setup>
import { reactive } from "vue";
import { ref } from "vue";
import ProduitsList from "./components/ProduitsList.vue";
import ProduitFrig from "./components/ProduitFrig.vue";
import ProduitResearch from "./components/ProduitResearch.vue";

let state = reactive({
  prod: { nom: "choux", qte: 2 },
  search: "",
});
function handlerRec(mot) {
  state.search = mot;
  
}

const open=ref(false);
function porte(){
  open.value =! open.value;
}
</script>

<template>
  <header>
    <nav>
      <ul> 
        <li class="recherche">
          <ProduitResearch @handlerr="(m) => (state.search = m)" />
        </li>
        <li class="ajoutProduit">
          <ProduitFrig @handlerp="(p) => (state.prod = { ...p })" />
        </li>
      </ul>
    </nav>
  </header>
  <button @click="state.search = ''" id="produits">Mon frigo</button>

  <div v-if="open" id="frigOuvert"> 
      <img id="pOuverte" @click="porte()" src="./assets/images/frigo-ouvert.png"> 
  <form>
    <div class="frigo-compose">
      <ProduitsList :prod="state.prod" :search="state.search" />
    </div>
  </form>
  </div>
  <div v-else id="frigoFermé">
    <img id="pClose" @click="porte()" src="./assets/images/frigo-fermé.png" >
  </div>
</template>

<style>
body {
  background-color: antiquewhite;
  font-family: "Arial";
}

#pClose{
  width: 300px;
  height: 500px;
}

.pOuverte{
  width: 600px;
  height: 650px;
}


#produits {
  margin-top: 15px;
  margin-left: 670px;
  color: #000000;
  font-size: 50px;
  border: none;
  background-color: transparent;
}
#produits:hover {
  color: #31302f;
}

ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
  background-color: #33493d;
  height: 100px;
  margin-top: 0px;
}

.recherche {
  text-align: center;
  float: left;
  height: 100px;
  margin: 25px 0 0 0;
  padding: 14px 0 0 20px;
}

#ajoutProd {
  background-image: url("assets/images/ajout-panier.png");
  background-size: cover;
  border: none;
  width: 24px;
  height: 24px;
  cursor: pointer;
  margin-left: 10px;
}

.ajoutProduit {
  text-align: center;
  float: right;
  height: 100px;
  margin: 25px 0 0 0;
  padding: 14px 0 0 20px;
}

form {
  float: right;
  margin-right: 150px;
}

#ajouter {
  background-image: url("assets/images/ajout-panier.png");
  background-size: cover;
  width: 30px;
  height: 30px;
  border-radius: 5px;
  border: none;
  cursor: pointer;
  background-color: #fcfcfc;
  margin-left: 30px;
}


#ajout {
  border: 1.5px solid #dc8e54;
  border-radius: 4px;
  margin-right: 20px;
}
#qte {
  border: 1.5px solid #dc8e54;
  border-radius: 4px;
}

/* The Close Button */
.close {
  color: #aaa;
  float: right;
  font-size: 28px;
  font-weight: bold;
}
.close:hover,
.close:focus {
  color: black;
  text-decoration: none;
  cursor: pointer;
}

.frigo-compose {
  margin-top: 20px;
  width: 500px;
  height: 75vh;
}

table {
  width: 100%;
}
th {
  background-color: #3a6b50;
  color: #ebeff1;
  border-bottom: 1px solid #000000;
}
th,
td {
  border: 1px solid #000000;
  text-align: center;
}
tr {
  height: 50px;
}
tr:hover {
  background-color: #76c79b;
}
td {
  color: black;
}

.buttonsup {
  background-image: url("assets/images/supprimer.png");
  background-size: cover;
  width: 25px;
  height: 20px;
  border-radius: 5px;
  border: none;
  cursor: pointer;

}

.buttonadd {
  background-image: url("assets/images/icon-plus.png");
  background-size: cover;
  width: 20px;
  height: 20px;
  border-radius: 5px;
  border: none;
  cursor: pointer;
  margin-right: 8px;
}

.buttonPanier{
  background-image:url("assets/images/ajout-panier.png");
  background-size: cover;
  width: 22px;
  height: 22px;
  border-radius: 5px;
  border: none;
  cursor: pointer;
  padding: 5px 5px 5px 5px;
  
}

.buttonremove {
  background-image: url("assets/images/icon-moins.png");
  background-size: cover;
  width: 20px;
  height: 20px;
  border-radius: 5px;
  border: none;
  cursor: pointer;
  margin-right: 8px;
}

</style>