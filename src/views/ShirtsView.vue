<template>
  <div style="text-align: center;">
    <h1 style="color: black;">Boutique</h1>
    <p style="color: black"> Nombre de produits : {{nbr_produits}}</p>
    <a v-if="!liste_produits_count" :href="new_page"><img src="../assets/fleche-droite.png" style="width: 50px; float: right; margin:-20; bottom: 0;"></a>
    <a v-if="hide_back_btn" :href="new_page_prec"><img src="../assets/fleche-gauche.png" style="width: 50px; float: left; margin:-20; bottom: 0;"></a>
  </div>
  <div v-if="!liste_produits_count" style="margin-top: 2em; display: grid;grid-template-columns: repeat(3, 1fr);">
    <div v-for="produit in liste_produits" style="background-color: white; padding: 30px; width: 269px; border-radius: 10px; margin-top: 10px;">
    <a :href="'/tee_shirt/' + produit.id">
      <h1 v-if="produit.flag == 'NEW'" style="text-align: center; color: white; background-color: red; width: 52px; border-radius: 50px; font-size: 15px; margin-left: 10em; float: right; width: 80px; margin:-20;">{{ produit.flag }}</h1>
      <h1 v-if="produit.flag == 'Sale!'" style="text-align: center; color: white; background-color: red; width: 52px; border-radius: 50px; font-size: 15px; margin-left: 10em; float: right; width: 80px; margin:-20;">{{ produit.flag }}</h1>
      <img style="width: 200px;" :src="produit.imageURL" />
      <div>
        <h2 style="text-align: center; white-space: nowrap; overflow: hidden; text-overflow: ellipsis;">{{ produit.name }}</h2>
        <h4 style="text-align: center; font-size: 18px; margin-top: 0.5em; margin-bottom: 0.5em;">{{ produit.price }}</h4>
        <h1 style="text-align: center; color: white; background-color: orange; width: 100px; border-radius: 50px; font-size: 15px;padding: 10px; margin-left: 3.5em;">Acheter</h1>
      </div>
      </a>
    </div>
  </div>
</template>

<style>
</style>

<script>
import ax from 'axios'
export default {
    data() {
        var new_page = parseInt(this.$route.params.page) + 1;
        if (new_page == 1) {
          var hide_back_btn = false;
        }else{
          var hide_back_btn = true;
        }
        return {
          liste_produits: null,
          liste_produits_count: false,
          nbr_produits: null,
          new_page: new_page,
          hide_back_btn: hide_back_btn,
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
            self.hide_back_btn = true;
            self.liste_produits_count = true;
            self.new_page_prec = self.new_page - 2;
          }else{
            self.new_page_prec = self.new_page - 2;
          }
        })
    }
}
</script>
