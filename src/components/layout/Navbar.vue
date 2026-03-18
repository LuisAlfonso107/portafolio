<script setup>
defineProps({
  items: {
    type: Array,
    default: () => [],
  },
})
</script>

<template>
  <header class="site-header">
    <nav class="navbar container">
      <a class="brand" href="#hero">NECROMANCER.dev</a>
      <div class="nav-links">
        <a
          v-for="item in items"
          :key="item.href"
          class="nav-link"
          :href="item.href"
        >
          {{ item.label }}
        </a>
      </div>
    </nav>
  </header>
</template>
