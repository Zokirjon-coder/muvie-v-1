<script setup>
import { ref } from 'vue';
import { useFetch } from '@/hooks/useFetch';
import BackgroundWithDot from '@/components/BackgroundWithDot.vue';

const count = ref(1);
const { data } = useFetch('https://jsonplaceholder.typicode.com/users');
console.log(data);
</script>

<template>
  <header></header>
  <main class="container mt-5">
    <BackgroundWithDot />
    <details>
      <summary>btn</summary>
      <ul>
        <li>line 1</li>
        <li>line 1</li>
        <li>line 1</li>
        <li>line 1</li>
      </ul>
    </details>
    <button type="button" class="btn btn-outline-primary" @click="count++">
      Count: {{ count }}
      <i class="fa fa-heart text-danger" />
    </button>

    <div class="mt-5">
      <i v-for="item in Array(count)" class="fa fa-heart text-danger" />
    </div>

    <div class="mt-5">
      <div v-for="item in data" class="text-danger">
        {{ item?.name || '' }}
        <a :href="item?.website" target="_blank">
          <i class="fa fa-arrow-right" />
        </a>
      </div>
    </div>
  </main>
</template>

<style scoped></style>
