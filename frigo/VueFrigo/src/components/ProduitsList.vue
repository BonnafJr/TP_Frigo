<script setup>
  import { reactive, ref, watch, onMounted } from "vue";
  // lien de l'API
  const url = "https://webmmi.iut-tlse3.fr/~pecatte/frigo/public/27/produits";
  let fetchOptions = { method: "GET" };
  const props = defineProps(["prod", "search"]);

  let lProduits = reactive({ liste: [] });

  // on fait une nouvelle requete ajax pour chaque changement de props
  watch(
    () => props.prod,
    (p_new, p_prec) => {
      addProduit(p_new);
    }
  );
  watch(
    () => props.search,
    (mot) => {
      console.log("mot:" + mot);
      getProduits(mot);
    }
  );

  // fonction pour chercher un produit
  function getProduits(mot) {
    fetch(url, fetchOptions)
      .then((response) => {
        return response.json();
      })
      .then((dataJSON) => {
        console.log(dataJSON);
        lProduits.liste = [...dataJSON].filter((p) => p.nom.includes(mot));
      })
      .catch((error) => {
        console.log(error.message);
      });
  }

  // fonction pour mettre à jour un produit
  function updateProduit(produit) {
    let myHeaders = new Headers();
    myHeaders.append("Content-Type", "application/json");
    const fetchOptions = {
      method: "PUT",
      headers: myHeaders,
      body: JSON.stringify(produit),
    };
    fetch(url, fetchOptions)
      .then((response) => {
        return response.json();
      })
      .then((dataJSON) => {
        getProduits("");
      })
      .catch((error) => console.log(error));
  }

  //fonction pour ajouter un produit
  function addProduit(produit) {
    let myHeaders = new Headers();
    myHeaders.append("Content-Type", "application/json");
    const fetchOptions = {
      method: "POST",
      headers: myHeaders,
      body: JSON.stringify(produit),
    };
    fetch(url, fetchOptions)
      .then((response) => {
        return response.json();
      })
      .then((dataJSON) => {
        console.log(dataJSON);
        getProduits("");
      })
      .catch((error) => console.log(error));
  }

  //fonction pour sup un produit
  function delProduit(id) {
    const fetchOptions = {
      method: "DELETE",
    };
    fetch(url + "/" + id, fetchOptions)
      .then((response) => {
        return response.json();
      })
      .then((dataJSON) => {
        getProduits("");
      })
      .catch((error) => console.log(error));
  }


  function handlerDelete(index) {
    delProduit(lProduits.liste[index].id);
  }

  function handlerAddOne(index) {
    lProduits.liste[index].qte++;
    updateProduit(lProduits.liste[index]);
  }

  function handlerRemoveOne(index) {
    lProduits.liste[index].qte--;
    if (lProduits.liste[index].qte == 0) handlerDelete(index);
    else updateProduit(lProduits.liste[index]);
  }

  onMounted(() => getProduits(""));
  </script>

  <template>
    <p v-if="props.search != ''">
      Les aliments de notre frigo recherchés :
    </p>
    <p v-else>Liste des produits du frigo</p>

    <table id="listeProduits">
      <tr>
        <th>Produits</th>
        <th>Quantité</th>
        <th>Événement</th>
      </tr>
      <tr v-for="(produit, index) in lProduits.liste" :key="produit.id">
        <td>{{ produit.nom }}</td>
        <td>{{ produit.qte }}</td>
        <td>
          <input
            type="button"
            name="ajouter1"
            @click="handlerAddOne(index)"
            class="buttonadd"
          />
          <input
            type="button"
            name="enlever1"
            @click="handlerRemoveOne(index)"
            class="buttonremove"
          />
          <input
            type="button"
            name="supprimer"
            @click="handlerDelete(index)"
            class="buttonsup"
          />
        </td>
      </tr>
    </table>
  </template>

<style>
</style>