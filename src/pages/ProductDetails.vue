<template>
  <section>
    <h2>{{ title }}</h2>
    <h3>${{ price}}</h3>
    <p>{{ description}}</p>
    <router-link to="/products/p2">Products 2</router-link>
  </section>
</template>

<script setup>
import { ref, inject, computed } from 'vue';
import { useRoute, useRouter } from 'vue-router';

const route = useRoute();
const router = useRouter();
// const link = useLink();

console.log(route);
console.log(router.getRoutes());
// console.log(link);

const products = inject('products');

const title = ref('');
const price = ref(null);
const description = ref('');

const selectedProduct = computed(() => {
   return products.value.find(product => product.id === route.params.pid);
});

title.value = computed(() => selectedProduct.value.title);
price.value = computed(() => selectedProduct.value.price);
description.value = computed(() => selectedProduct.value.description);
</script>


<style scoped>
section {
  margin: 3rem auto;
  max-width: 40rem;
  padding: 1rem;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
}
</style>