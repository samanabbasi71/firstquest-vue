<template>
    <div>
        <Item v-for="(tour, index) in tours" :key="index" :tour="tour"/>
    </div>
</template>

<script>
import Item from '@/components/tour/item';

export default {
    components: {
        Item
    },
    props: {
        tours: {
            type: Array,
            default: () => ([])
        }
    }
}
</script>

<style>

</style>