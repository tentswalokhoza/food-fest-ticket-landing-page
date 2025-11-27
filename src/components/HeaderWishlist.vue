<template>
  <header class="site-header">
    <div class="brand">
        <h2>Cape Town Food Fest</h2>
        <p class="tag">Annual food festival · Tickets & experiences</p>
      </div>

    <div class="wishlist">
      <button class="wish-btn" aria-label="View wishlist">
        ❤️ <span class="count">{{ count }}</span>
      </button>
    </div>
  </header>
</template>

<script setup>
defineProps({ count: { type: [Number], default: 0 } })
</script>

<style scoped>
.site-header {
  display:flex; align-items:center; justify-content:space-between; gap:1rem; margin-bottom:1rem;
}
.brand h2 { margin:0; color: var(--brand-gold) }
.tag { margin:0; color: var(--color-text-muted); font-size:0.9rem }
.wish-btn { border:0; background:transparent; font-size:1rem; cursor:pointer; color: var(--color-text) }
.count { font-weight:700; margin-left:0.35rem; color: var(--brand-gold) }
</style>
