<template>
  <div class="app">
    <header class="app__header">
      <div class="app__header-inner">
        <div class="app__title-block">
          <h1 class="app__title">🤖 AI Tools Directory</h1>
          <p class="app__subtitle">
            Discover the best AI tools across every category — curated and organised for creators, developers, and researchers.
          </p>
        </div>
        <div class="app__search-wrap">
          <input
            v-model="searchQuery"
            class="app__search"
            type="search"
            placeholder="Search tools, categories, tags…"
            aria-label="Search AI tools"
          />
        </div>
        <nav class="app__nav" aria-label="Categories">
          <a
            v-for="cat in visibleCategories"
            :key="cat.id"
            :href="`#${cat.id}`"
            class="app__nav-link"
          >
            <span>{{ cat.icon }}</span> {{ cat.name }}
          </a>
        </nav>
      </div>
    </header>

    <main class="app__main">
      <template v-if="visibleCategories.length > 0">
        <CategorySection
          v-for="cat in visibleCategories"
          :key="cat.id"
          :category="cat"
          :search="searchQuery"
        />
      </template>
      <div v-else class="app__empty">
        <p>😕 No tools found for "<strong>{{ searchQuery }}</strong>"</p>
        <button class="app__clear-btn" @click="searchQuery = ''">Clear search</button>
      </div>
    </main>

    <footer class="app__footer">
      <p>Built with Vue 3 · {{ totalTools }} tools across {{ categories.length }} categories</p>
    </footer>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";
import { categories } from "./data/tools.js";
import CategorySection from "./components/CategorySection.vue";

const searchQuery = ref("");

const totalTools = computed(() =>
  categories.reduce((sum, cat) => sum + cat.tools.length, 0)
);

const visibleCategories = computed(() => {
  const q = searchQuery.value.toLowerCase().trim();
  if (!q) return categories;
  return categories
    .map((cat) => ({
      ...cat,
      tools: cat.tools.filter(
        (tool) =>
          tool.name.toLowerCase().includes(q) ||
          tool.description.toLowerCase().includes(q) ||
          tool.tags.some((tag) => tag.toLowerCase().includes(q))
      ),
    }))
    .filter((cat) => cat.tools.length > 0);
});
</script>

<style scoped>
.app {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

.app__header {
  background: var(--color-header-bg);
  border-bottom: 1px solid var(--color-border);
  padding: 2rem 1rem 1.25rem;
  position: sticky;
  top: 0;
  z-index: 100;
  backdrop-filter: blur(12px);
}

.app__header-inner {
  max-width: 1200px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.app__title {
  font-size: 1.75rem;
  font-weight: 800;
  color: var(--color-text-primary);
  margin: 0;
  letter-spacing: -0.02em;
}

.app__subtitle {
  font-size: 0.9rem;
  color: var(--color-text-secondary);
  margin: 0.25rem 0 0;
  max-width: 600px;
}

.app__search {
  width: 100%;
  padding: 0.65rem 1rem;
  font-size: 0.95rem;
  border: 1px solid var(--color-border);
  border-radius: 999px;
  background: var(--color-input-bg);
  color: var(--color-text-primary);
  outline: none;
  transition: border-color 0.2s, box-shadow 0.2s;
  box-sizing: border-box;
}

.app__search:focus {
  border-color: var(--color-accent);
  box-shadow: 0 0 0 3px var(--color-accent-focus);
}

.app__nav {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.app__nav-link {
  display: inline-flex;
  align-items: center;
  gap: 0.3rem;
  padding: 0.3rem 0.75rem;
  border-radius: 999px;
  font-size: 0.8rem;
  font-weight: 500;
  background: var(--color-tag-bg);
  color: var(--color-tag-text);
  text-decoration: none;
  transition: background 0.2s, color 0.2s;
}

.app__nav-link:hover {
  background: var(--color-accent);
  color: #fff;
}

.app__main {
  flex: 1;
  max-width: 1200px;
  width: 100%;
  margin: 0 auto;
  padding: 2.5rem 1rem;
}

.app__empty {
  text-align: center;
  padding: 4rem 1rem;
  color: var(--color-text-secondary);
  font-size: 1.05rem;
}

.app__clear-btn {
  margin-top: 1rem;
  padding: 0.5rem 1.25rem;
  border-radius: 999px;
  border: 1px solid var(--color-border);
  background: transparent;
  color: var(--color-text-primary);
  font-size: 0.875rem;
  cursor: pointer;
  transition: background 0.2s;
}

.app__clear-btn:hover {
  background: var(--color-tag-bg);
}

.app__footer {
  text-align: center;
  padding: 1.5rem 1rem;
  font-size: 0.8rem;
  color: var(--color-text-muted);
  border-top: 1px solid var(--color-border);
}
</style>
