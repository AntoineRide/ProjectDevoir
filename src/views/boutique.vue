<template>
  <div style="text-align: center;">
      <h1 style="color: black;">Boutique</h1>

      <p style="color: black"> Nombre de produits : {{nbr_produits}}</p>
      
      <a v-if="!liste_produits_count" :href="new_page"><img src="../assets/fleche-droite.png" class="fleche_right"></a>
      <a v-if="hide_button" :href="new_page_prec"><img src="../assets/fleche-gauche.png" class="fleche_left"></a>
  </div>

  <div v-if="!liste_produits_count" class="case_boutique">
      <div v-for="produit in liste_produits" class="back_case">
          
          <a :href="'/tee_shirt/' + produit.id">
            
            <h1 v-if="produit.flag == 'NEW'" class="flag_new">{{ produit.flag }}</h1>
            <h1 v-if="produit.flag == 'Sale!'" class="flag_sale">{{ produit.flag }}</h1>
            
            <img style="width: 200px;" :src="produit.imageURL" />
            
            <div>
                <h2 class="produit_name">{{ produit.name }}</h2>
                <h4 class="produit_price">{{ produit.price }}</h4>
                <h1 class="bouton_buy">Acheter</h1>
            </div>
          </a>
      </div>
  </div>
</template>

<style>
.fleche_right {
  width: 50px; 
  float: right; 
  margin:-20; 
  bottom: 0;

}

.fleche_left {
  width: 50px; 
  float: left; 
  margin:-20; 
  bottom: 0;

}

.case_boutique {
  margin-top: 2em; 
  display: grid;
  grid-template-columns: repeat(3, 1fr);
}

.back_case {
  background-color: rgb(228, 228, 228); 
  border: 2px solid black;
  padding: 30px; 
  width: 269px; 
  border-radius: 10px; 
  margin-top: 10px;

}

.flag_new {
  text-align: center; 
  color: white; 
  background-color: red; 
  width: 52px; 
  border-radius: 50px; 
  font-size: 15px; 
  margin-left: 10em; 
  float: right; 
  width: 80px; 
  margin:-20;
}

.flag_sale {
  text-align: center; 
  color: white; 
  background-color: red; 
  width: 52px; 
  border-radius: 50px; 
  font-size: 15px; 
  margin-left: 10em; 
  float: right; 
  width: 80px; 
  margin:-20;
}

.produit_name {
  text-align: center; 
  white-space: nowrap; 
  overflow: hidden; 
  text-overflow: ellipsis;
}
.produit_price {
  text-align: center; 
  font-size: 18px; 
  margin-top: 0.5em; 
  margin-bottom: 0.5em;
}
.bouton_buy {
  text-align: center; 
  color: white; 
  background-color: orange; 
  width: 100px; 
  border-radius: 50px; 
  font-size: 15px;
  padding: 10px; 
  margin-left: 3.5em;
}

</style>

<script>
import ax from 'axios'
export default {
    data() {
        var new_page = parseInt(this.$route.params.page) + 1;
        if (new_page == 1) {
          var hide_button = false;
        }else{
          var hide_button = true;
        }
        return {
          liste_produits: null,
          liste_produits_count: false,

          nbr_produits: null,

          new_page: new_page,

          hide_button: hide_button,
        }
    },
    mounted() {
      let self = this
      ax
        .get('http://vps-a47222b1.vps.ovh.net/TShirt/page/' + this.new_page)
        .then(function (response) {
          self.liste_produits = response.data
          self.nbr_produits = self.liste_produits.length
          if (self.liste_produits.length == 0) {
            self.hide_button = true;
            self.liste_produits_count = true;
            self.new_page_prec = self.new_page - 2;
          }else{
            self.new_page_prec = self.new_page - 2;
          }
        })
    }
}
</script>
