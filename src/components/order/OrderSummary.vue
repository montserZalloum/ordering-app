<template>
    <div class="order-summary">
        <div class="flex gap-y-8 flex-col px-6 pb-8">
            <template v-if="items.length > 0">
                <ItemInfo v-for="item in items" :key="item.id" :item="item" />
            </template>
            <div v-else class="text-center">No items</div>
        </div>
        <div class="order-total pt-10 border-black border-t px-6">
            <ItemInfo :total="totalItemsPrice" />
        </div>
    </div>
</template>

<script>
    import ItemInfo from './ItemInfo.vue'
    import {bus} from '../../main'
    export default {
        emits: ['update-place-order'],
        components: {ItemInfo},
        data: () => ({
            items: [],
            total: 0,
        }),
        created(){
            bus.$on('add-to-cart', (item) => {
                const itemIndex = this.items.findIndex((i)=>i.id == item.id);
                if (itemIndex > -1) {
                    this.items[itemIndex].quantity += +item.quantity;
                } else {
                    this.items.push(item);
                }
                this.$emit('update-place-order',this.items);
            })
        },
        computed: {
            totalItemsPrice() {
                return this.items.reduce((total, item) => total + item.quantity * item.Price, 0);
            }
        }
    }
</script>
