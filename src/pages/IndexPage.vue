<script lang="ts">
import { api } from 'src/boot/axios';
import { onBeforeMount, ref } from 'vue';
export default { name: 'IndexPage' };
</script>
<script setup lang="ts">
const info = ref<unknown[]>([]);

const getData = async () => {
  console.log('getData');

  const { data } = await api.get(
    import.meta.env.DEV ? '/pokemon/ditto' : 'quotes'
  );

  console.log(data);

  info.value = import.meta.env.DEV ? data.abilities : data;
};

onBeforeMount(async () => await getData());

const apiUrl = import.meta.env.VITE_API_URL;
</script>

<template>
  <q-page class="column justify-center items-center">
    <h4>{{ apiUrl }}</h4>

    <pre> {{ info }} </pre>
  </q-page>
</template>

<style lang="scss" scoped></style>
