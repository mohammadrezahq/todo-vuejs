<template>
  <router-link :to="url" class="flex items-center p-2">
    <svg
      xmlns="http://www.w3.org/2000/svg"
      aria-hidden="true"
      role="img"
      width="1em"
      height="1em"
      preserveAspectRatio="xMidYMid meet"
      viewBox="0 0 20 20"
    >
      <path fill="currentColor" d="m14 5l-5 5l5 5l-1 2l-7-7l7-7z" />
    </svg>
    {{ title }}
  </router-link>
</template>
<script>
export default {
  props: ["url", "title"],
};
</script>