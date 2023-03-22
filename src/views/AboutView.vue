<script >
import InventoryCards from '../components/InventoryCards.vue'

export default {
   components:{
    InventoryCards
   }
}
</script>

<template>
  <main>
    <InventoryCards :userInventory="userInventory" />
  </main>
</template>
