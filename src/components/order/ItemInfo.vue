<template>
  <div class="prod-info flex justify-between">
    <p class="font-base font-light truncate">
      <span class="mr-2" v-if="item">{{ +item.quantity }}X {{ item.name }}</span>
      <span class="mr-2 font-bold" v-else>Total</span>
    </p>
    <p class="font-base font-light whitespace-nowrap" :class="{'font-bold':total}">{{ totalPrice }} SAR</p>
  </div>
</template>

<script>
export default {
  props: ["item","total"],
  computed: {
      totalPrice(){
        return this.item ? this.item.quantity * this.item.Price : this.total;
      }
  }
};
</script>
