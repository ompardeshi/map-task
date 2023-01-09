<template>
  <div class="h-screen w-full bg-zinc-800 p-10">
    <div class="bg-black h-full p-5 rounded-2xl">
      <Map class="h-full rounded-lg overflow-hidden"></Map>
    </div>
  </div>

</template>

<script setup>

import InstantSearch from 'vue-instantsearch/vue3/es';

// ...
app.use(InstantSearch);

</script>