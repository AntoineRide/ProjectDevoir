<template>
  <div style="text-align: center; display: flex; justify-content: space-between; align-items: center;">
    <img style="width: 400px;" :src="infoProduit.imageURL"/>
    <div style="text-align: left; justify-content: space-between;">
        <H1 style="color: black; text-align: center; top:20;">{{infoProduit.name}}</H1>
        <p style="color: black; text-align: center;">{{infoProduit.description}}</p>
        <p style="color: black text-align: center; font-size: 18px; margin-top: 0.5em; margin-bottom: 0.5em;">{{infoProduit.price}}</p>
        <div style="background-color: orange; width: 150px; border-radius: 25px; float: right; margin:-20; bottom: 0;">
          <h1 style="text-align: center; color: white;">Acheter</h1>
        </div>
    </div>
  </div>
  
</template>

<style>
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
