<script setup>
import WelcomeItem from './WelcomeItem.vue'
import product from './product.vue'
import DocumentationIcon from './icons/IconDocumentation.vue'
import ToolingIcon from './icons/IconTooling.vue'
import EcosystemIcon from './icons/IconEcosystem.vue'
import CommunityIcon from './icons/IconCommunity.vue'
import SupportIcon from './icons/IconSupport.vue'
</script>

<template>
  <WelcomeItem>
    <template #heading>nos produits phares</template>
  
  </WelcomeItem>

  <product>
    <template #image></template>
  

  
  </product>

  <product>
    <template #image>Ecosystem</template>

  </product>

  <product>
    <template #image>Community</template>


  </product>

  <product>
    <template #image>Support Vue</template>

  </product>
</template>
