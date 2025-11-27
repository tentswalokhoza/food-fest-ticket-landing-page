<script setup>
import { reactive, computed } from 'vue'
import HeaderWishlist from './components/HeaderWishlist.vue'
import CourseCard from './components/CourseCard.vue'

const state = reactive({
  courses: [
    { id: 1, title: 'Sourdough Basics', chef: 'Ana Rossi', level: 'Beginner', price: 49, available: true, image: '/images/sourdough.svg' },
    { id: 2, title: 'Mastering Risotto', chef: 'Marco Leoni', level: 'Intermediate', price: 69, available: true, image: '/images/risotto.svg', featured: true },
    { id: 3, title: 'French Pastry Secrets', chef: 'Claire Dupont', level: 'Advanced', price: 99, available: false, image: '/images/pastry.svg' },
    { id: 4, title: 'Vegan Comfort Classics', chef: 'Sam Patel', level: 'Beginner', price: 39, available: true, image: '/images/vegan.svg' },
    { id: 5, title: 'Seafood on Fire', chef: 'Liu Wei', level: 'Advanced', price: 119, available: false, image: '/images/seafood.svg' },
    { id: 6, title: 'Weeknight Pasta', chef: 'Giulia Ferri', level: 'Intermediate', price: 59, available: true, image: '/images/pasta.svg' }
  ],
  wishlist: new Set()
})

const filters = reactive({ level: 'All', availability: 'All', q: '' })

const levels = computed(() => {
  const set = new Set(state.courses.map(c => c.level))
  return ['All', ...Array.from(set)]
})

const filteredCourses = computed(() => {
  return state.courses.filter(c => {
    if (filters.level !== 'All' && c.level !== filters.level) return false
    if (filters.availability === 'Available' && !c.available) return false
    if (filters.availability === 'Sold Out' && c.available) return false
    if (filters.q && !(`${c.title} ${c.chef}`.toLowerCase().includes(filters.q.toLowerCase()))) return false
    return true
  })
})

function toggleSave(id) {
  if (state.wishlist.has(id)) state.wishlist.delete(id)
  else state.wishlist.add(id)
}

const wishlistCount = computed(() => state.wishlist.size)

function formatPrice(value) {
  return new Intl.NumberFormat('en-ZA', { style: 'currency', currency: 'ZAR' }).format(value)
}
</script>

<template>
  <div>
    <HeaderWishlist :count="wishlistCount" />

    <main>
      <section class="intro">
        <h1>Cooking Masterclass — Course Catalogue</h1>
        <p class="lead">Discover curated workshops from experienced chefs. Save classes you like to your wishlist.</p>
      </section>

      <section class="filters">
        <div class="filter-group">
          <label for="level">Level</label>
          <select id="level" v-model="filters.level">
            <option v-for="l in levels" :key="l" :value="l">{{ l }}</option>
          </select>
        </div>

        <div class="filter-group">
          <label for="availability">Availability</label>
          <select id="availability" v-model="filters.availability">
            <option value="All">All</option>
            <option value="Available">Available</option>
            <option value="Sold Out">Sold Out</option>
          </select>
        </div>

        <div class="filter-group search">
          <label for="q">Search</label>
          <input id="q" v-model="filters.q" placeholder="Search title or chef" />
        </div>
      </section>

      <section class="catalogue">
        <div class="grid">
          <CourseCard
            v-for="course in filteredCourses"
            :key="course.id"
            :course="course"
            :saved="state.wishlist.has(course.id)"
            @toggle-save="toggleSave"
            :formatPrice="formatPrice"
          />
        </div>
      </section>
    </main>
  </div>
</template>

<style scoped>
h1 {
  font-size: 1.6rem;
  margin-bottom: 0.25rem;
}

.lead {
  color: var(--color-text-muted);
  margin-bottom: 1.25rem;
}

.catalogue .grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 1rem;
}

@media (min-width: 640px) {
  .catalogue .grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (min-width: 1024px) {
  .catalogue .grid {
    grid-template-columns: repeat(3, 1fr);
  }
}

main {
  margin-top: 1rem;
}

.intro {
  margin-bottom: 1rem;
}

.filters {
  display:flex;
  gap:1rem;
  align-items:end;
  margin-bottom:1rem;
  flex-wrap:wrap;
}
.filter-group { display:flex; flex-direction:column; gap:0.25rem }
.filter-group label { font-size:0.85rem; color: var(--color-text-muted) }
.filter-group select,
.filter-group input { background: var(--color-background); color: var(--color-text); border:1px solid var(--color-border); padding:6px 8px; border-radius:6px }
.filter-group.search { flex:1; min-width:160px }

</style>
