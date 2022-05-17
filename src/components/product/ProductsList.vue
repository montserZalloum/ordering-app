<template>
    <div>
        <div v-if="products.length > 0" class="product-list grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-16 ">
            <ItemCard
                @add-to-cart="showItemDetails"
                class="w-full"
                v-for="product in products"
                :key="product.id"
                :item="product"
            />
            <Modal @close="toggleProductModal" :show="showItemModal">
                <ItemCardModal @close="toggleProductModal" :item="product" />
            </Modal>
        </div>
        <div v-else class="flex justify-center">
            <Loader />
        </div>
  </div>
</template>

<script>
import ItemCard from "../base/ItemCard.vue";
import ItemCardModal from "../base/ItemCard_Modal.vue";
import Modal from "../base/Modal.vue";
import Loader from "../base/PageLoader.vue";
import config from '../../../config'
export default {
  components: {
    ItemCard,
    Modal,
    ItemCardModal,
    Loader
  },
  created() {
    this.getProducts();
  },
  data: () => ({
    products: [],
    showItemModal: false,
    product: {},
  }),
  methods: {
    showItemDetails(item) {
      this.product = item;
      this.toggleProductModal();
    },
    toggleProductModal() {
      this.showItemModal = !this.showItemModal;
    },
    async getProducts() {
      this.products = await ((await fetch(`${config.API_URL}/products`)).json())
    },
  },
};
</script>
