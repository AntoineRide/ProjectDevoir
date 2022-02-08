<template>
  <div class="align_item">
    <img style="width: 400px;" :src="infoProduit.imageURL"/>
    <div>
        <H1 class="nom_produit">{{infoProduit.name}}</H1>
        <p class="desc_produit">{{infoProduit.description}}</p>
        <p class="prix_produit">{{infoProduit.price}}</p>
        <div class="back_buy">
          <h1 class="buttom_buy">Acheter</h1>
        </div>
    </div>
  </div>
  
</template>

<style>
.align_item {
  text-align: center; 
  display: flex; 
  justify-content: space-between; 
  align-items: center;
}
.nom_produit {
  color: black; 
  text-align: center; 
  top:20;
}
.desc_produit {
  color: black; 
  text-align: center;
}
.prix_produit {
  color: black; 
  text-align: center; 
  font-size: 18px; 
  margin-top: 0.5em; 
  margin-bottom: 0.5em;
}
.back_buy {
  background-color: orange; 
  width: 150px; 
  border-radius: 25px; 
  float: right; 
  margin:-20; 
  bottom: 0;
}
.buttom_buy {
  text-align: center; 
  color: white;
}
</style>

<script>
import ax from 'axios'
export default {
    data() {
        var id_produit = this.$route.params.id;
        return {
          id_produit: id_produit,
          infoProduit: ""
        }
    },
    mounted() {
      let self = this
      ax
        .get('http://vps-a47222b1.vps.ovh.net/TShirt/' + this.id_produit)
        .then(function (response) {
          self.infoProduit = response.data
        })
    }
}
</script>
