<template>
  <div class="item-card group relative cursor-pointer" @click="addToCart">
    <div
      class="w-full rounded-md overflow-hidden group-hover:opacity-75 duration-300"
    >
      <img
        :src="`${item.image}?random=${item.createdAt}`"
        :alt="item.name"
        class="w-full h-full object-center object-cover lg:w-full lg:h-full"
      />
    </div>
    <div class="mt-4 flex justify-between">
      <div>
        <h3 class="text-sm text-gray-700">
          {{item.name}}
        </h3>
        <p class="text-sm font-medium text-gray-900">${{item.Price}}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  emits: ["add-to-cart"],
  props: ["item"],
  methods: {
    addToCart() {
      this.$emit("add-to-cart", this.item);
    },
  },
  mounted(){
    
  }
};
</script>
