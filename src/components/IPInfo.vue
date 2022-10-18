<template>
  <div
    class="absolute -bottom-64 lg:-bottom-20 flex flex-col lg:flex-row bg-white gap-y-4 gap-x-12 px-8 pt-8 pb-12 rounded-md"
  >
    <!-- flex item one -->
    <div class="flex flex-col">
      <h2 class="text-xs mb-2 uppercase">IP Address</h2>
      <span class="text-2xl">8.8.8.8</span>
    </div>
    <!-- flex item two -->
    <div class="flex flex-col">
      <h2 class="text-xs mb-2 uppercase">Location</h2>
      <span class="text-2xl">Lagos</span>
    </div>
    <!-- flex item three -->
    <div class="flex flex-col">
      <h2 class="text-xs mb-2 uppercase">Timezone</h2>
      <span class="text-2xl">UTC -07:00</span>
    </div>
    <!-- flex item four -->
    <div class="flex flex-col">
      <h2 class="text-xs mb-2 uppercase">ISP</h2>
      <span class="text-2xl">Reftek</span>
    </div>
  </div>
</template>

<script>
export default {
  setup() {
    return {};
  },
};
</script>
