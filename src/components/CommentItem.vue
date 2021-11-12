<template>
  <div class="flex">
    <img :src="avatar" alt="" class="w-12 h-12 mr-4 rounded-full"/>
    <div>
      <p>{{ user }}</p>
      <p class="text-gray-600 text-sm">{{ time }}</p>
    </div>
  </div>
  <p class="text-gray-600 py-4">
    {{ content }}
  </p>
</template>

<script setup>
defineProps([ "user", "avatar", "time", "content" ]);
</script>

<style>

</style>