<template>
    <div class="item-card relative">
      <svg @click="closeModal" xmlns="http://www.w3.org/2000/svg" class="h-8 w-8 text-red-400 absolute left-3 top-3 rounded-full bg-white cursor-pointer" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
        <path stroke-linecap="round" stroke-linejoin="round" d="M10 14l2-2m0 0l2-2m-2 2l-2-2m2 2l2 2m7-2a9 9 0 11-18 0 9 9 0 0118 0z" />
      </svg>
        <div class="w-full overflow-hidden h-60">
          <img :src="`${item.image}?random=${item.id}`" alt="Front of men&#039;s Basic Tee in black." class="w-full h-full object-center object-cover">
        </div>
        <div class="-mt-6 shadow-2xl shadow-red-400 pt-5 pb-3 px-5 bg-white w-full relative rounded-t-3xl">
            <div class="flex justify-between">
              <h3 class="text-lg font-light text-black">
                {{item.name}}
              </h3>
              <p class="text-3xl font-bold text-red-400 -mt-2">${{item.Price}}</p>
            </div>
            <p class="text-gray-500">{{item.description}}</p>
            <form @submit.prevent="submitForm" class="mt-5">
              <div class="relative flex rounded-md shadow-sm gap-2">
                  <input v-model="quantity" type="number" min="1" id="quantity" class="border-2 border-red-300  text-sm rounded-lg focus:ring-red-500 focus:border-red-500 block w-30 p-2.5   dark:placeholder-gray-300 dark:text-black dark:focus:ring-red-500 dark:focus:border-red-500" placeholder="Please add a quantity" required>
                  <button class="text-white bg-red-400 hover:bg-red-800 focus:ring-4 focus:outline-none focus:ring-red-300 font-medium rounded-lg text-sm w-full px-5 py-2.5 text-center dark:bg-red-600 dark:hover:bg-red-700 dark:focus:ring-red-800">Add To Cart</button>
              </div>
            </form>
        </div>
    </div>
</template>

<script>
    import {bus} from '../../main'
    export default {
      emits: ["close"],
      props:['item'],
      data:()=>({
        quantity: 1
      }),
      methods: {
        closeModal(){
          this.$emit('close')
        },
        submitForm(){
          bus.$emit('add-to-cart', {
            ...this.item,
            Price : +this.item.Price,
            quantity: +this.quantity
          })
          this.closeModal();
        }
      },
      mounted(){
        console.log(this.item.image)
      }
    }
</script>