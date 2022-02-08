<script>
import axios from 'vue-axios'
export default {
  name: 'app',
  data() {
    return {
      info: null
    }
  },
  mounted() {
      ax
        .get('http://vps-a47222b1.vps.ovh.net/TShirt/page/' + this.new_page)
        .then(function (response) {
          console.log(response);
         
        })
    }
}
</script>

<template>
    <div class="item">
    <div class="details" id="article-shop">
      
     <img name="image" src="src/assets/logo.svg" alt="" width="200" height="50" />
     <div id="app">
          {{ info }}
     </div>

      <slot></slot>
    </div>
  </div>
</template>

<style>

</style>