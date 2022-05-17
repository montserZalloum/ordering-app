<template>
    <aside class="right-side">
        <Card class="h-full">
            <ProductsList class="pt-5 px-4 lg:px-24" />
        </Card>
    </aside>
</template>

<script>
    import Card from './base/Card.vue'
    import ProductsList from './product/ProductsList.vue'
    export default {
        components: {
            Card,
            ProductsList
        },
    }
</script>
