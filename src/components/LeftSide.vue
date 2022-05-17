<template>
    <aside class="left-side">
        <Card class="h-full relative">
            <h1 class="text-center text-3xl font-normal tracking-wide border-b pb-5 border-black">Order Summery</h1>
            <OrderSummary @update-place-order="updateOrderBtn" class="pt-10 pb-8" />
            <button @click="placeOrder" :disabled="canPlaceOrder" class="bg-green-400 absolute bottom-0 py-5 w-full rounded-3xl text-white disabled:opacity-25">Place Order</button>
            
            <Modal @close="toggleAlertModal" :show="isAlertModalOpen">
                <Card>
                    <div class="flex items-center flex-col">
                        <h1 class="text-3xl text-center text-red-400 font-bold">{{alertMessage}}</h1>
                        <button @click="toggleAlertModal" class="bg-red-400 py-3 w-3/4 rounded-3xl text-white mt-5">Close</button>
                    </div>
                </Card>
            </Modal>
            <Loader :full="true" v-if="isLoading" />
        </Card>
    </aside>
</template>

<script>
    import Card from './base/Card.vue'
    import Modal from "./base/Modal.vue";
    import Loader from "./base/PageLoader.vue";
    import OrderSummary from './order/OrderSummary.vue'
    import config from '../../config'
    export default {
        components: {
            Card,
            Modal,
            OrderSummary,
            Loader
        },
        data:()=>({
            products: [],
            isAlertModalOpen: false,
            alertMessage:'Thank you for Choosing us',
            isLoading: false,
        }),
        computed: {
            canPlaceOrder() {
                return !this.products.length > 0;
            }
        },
        methods: {
            updateOrderBtn(items){
                this.products = items;
            },
            toggleAlertModal() {
                this.isAlertModalOpen = !this.isAlertModalOpen;
            },
             async placeOrder() {
                 this.isLoading = true;
                 try {
                     await fetch(`${config.API_URL}/orders`,{
                         method: 'POST',
                         headers: {
                             'Content-Type': 'application/json'
                         },
                         body: JSON.stringify({
                             payload: {
                                 products: this.products.map(i=>({
                                     id: i.id,
                                     quantity: i.quantity,
                                 }))
                             }
                         })
                     })
                 } catch(e) {
                     this.alertMessage = 'An Error Occured! Please try again later';
                 }
                 this.isLoading = false;
                 this.toggleAlertModal();
            }
        }
    }
</script>
