<template>
  <article class="card" :class="{ featured: course.featured }">
    <div class="media" :class="{ 'sold-out': !course.available }">
      <img v-if="course.image" :src="course.image" alt="" class="thumb" />
      <div v-else class="placeholder">🍳</div>
      <span v-if="!course.available" class="badge sold">Sold Out</span>
      <span v-if="course.featured" class="badge featured-badge">Featured</span>
    </div>

    <div class="content">
      <h3 class="title">{{ course.title }}</h3>
      <p class="meta">By <strong>{{ course.chef }}</strong> • <span class="level">{{ course.level }}</span></p>
      <div class="actions">
        <div class="price">{{ formatPrice(course.price) }}</div>
        <button class="save" :class="{ saved }" @click="$emit('toggle-save', course.id)">
          <span v-if="saved">✓ Saved</span>
          <span v-else>♡ Save</span>
        </button>
      </div>
    </div>
  </article>
</template>

<script setup>
defineProps({
  course: { type: Object, required: true },
  saved: { type: Boolean, default: false },
  formatPrice: { type: Function, required: true }
})
</script>

<style scoped>
.card {
  border: 1px solid var(--color-border);
  border-radius: 10px;
  overflow: hidden;
  background: var(--color-background-soft);
  display: flex;
  flex-direction: column;
}

.media {
  height: 110px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(135deg, rgba(212,175,55,0.06) 0%, rgba(239,230,200,0.03) 100%);
  position: relative;
}

.placeholder { font-size: 2rem; color: var(--brand-gold) }

.thumb { width: 100%; height: 110px; object-fit: cover; display:block }

.badge.sold {
  position: absolute;
  right: 0.5rem;
  top: 0.5rem;
  background: #555;
  color: white;
  padding: 0.25rem 0.5rem;
  border-radius: 6px;
  font-size: 0.8rem;
}

.badge.featured-badge {
  position: absolute;
  left: 0.5rem;
  top: 0.5rem;
  background: var(--brand-gold-dark);
  color: #0b0b0b;
  padding: 0.25rem 0.5rem;
  border-radius: 6px;
  font-size: 0.78rem;
  font-weight:700;
}

.content { padding: 0.75rem 1rem; display:flex; flex-direction:column; gap:0.5rem }
.title { font-size: 1.05rem; margin:0; color: var(--color-heading) }
.meta { color: var(--color-text-muted); font-size: 0.9rem }
.level { background: rgba(212,175,55,0.08); color: var(--brand-gold); padding: 2px 6px; border-radius: 6px; font-size:0.8rem }

.actions { display:flex; align-items:center; justify-content:space-between; margin-top:0.5rem }
.price { font-weight:700; color: var(--brand-gold) }
.save { border:0; background:transparent; cursor:pointer; padding:6px 10px; border-radius:8px; color: var(--color-text) }
.save.saved { color: var(--brand-gold); font-weight:700 }

.media.sold-out { filter: grayscale(60%); opacity: 0.95 }

.card.featured {
  border: 1px solid var(--brand-gold-dark);
  box-shadow: 0 6px 22px rgba(212,175,55,0.08);
  transform: translateY(-2px);
}
</style>
