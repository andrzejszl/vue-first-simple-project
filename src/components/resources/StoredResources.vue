<template>
    <ul>
        <resource-card v-for="item in items" :key="item.id" :item="item"></resource-card>
    </ul>
</template>

<script>
import ResourceCard from './ResourceCard.vue';
    export default {
        components: {ResourceCard},
        props: ['items']
    }
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
  margin: auto;
  max-width: 40rem;
}
</style>