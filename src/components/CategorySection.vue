<template>
  <section class="category" :id="category.id">
    <div class="category__header">
      <span class="category__icon">{{ category.icon }}</span>
      <div>
        <h2 class="category__name">{{ category.name }}</h2>
        <p class="category__description">{{ category.description }}</p>
      </div>
    </div>
    <div class="category__grid">
      <ToolCard v-for="tool in filteredTools" :key="tool.name" :tool="tool" />
    </div>
  </section>
</template>

<script setup>
import { computed } from "vue";
import ToolCard from "./ToolCard.vue";

const props = defineProps({
  category: {
    type: Object,
    required: true,
  },
  search: {
    type: String,
    default: "",
  },
});

const filteredTools = computed(() => {
  const q = props.search.toLowerCase().trim();
  if (!q) return props.category.tools;
  return props.category.tools.filter(
    (tool) =>
      tool.name.toLowerCase().includes(q) ||
      tool.description.toLowerCase().includes(q) ||
      tool.tags.some((tag) => tag.toLowerCase().includes(q))
  );
});
</script>

<style scoped>
.category {
  margin-bottom: 3rem;
}

.category__header {
  display: flex;
  align-items: flex-start;
  gap: 1rem;
  margin-bottom: 1.25rem;
}

.category__icon {
  font-size: 2rem;
  line-height: 1;
  flex-shrink: 0;
  margin-top: 0.1rem;
}

.category__name {
  font-size: 1.375rem;
  font-weight: 700;
  color: var(--color-text-primary);
  margin: 0 0 0.25rem;
}

.category__description {
  font-size: 0.875rem;
  color: var(--color-text-secondary);
  margin: 0;
}

.category__grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
  gap: 1rem;
}

@media (max-width: 720px) {
  .category {
    margin-bottom: 2rem;
  }

  .category__header {
    gap: 0.7rem;
    margin-bottom: 0.9rem;
  }

  .category__icon {
    font-size: 1.6rem;
  }

  .category__name {
    font-size: 1.1rem;
    margin-bottom: 0.15rem;
  }

  .category__description {
    font-size: 0.82rem;
  }

  .category__grid {
    grid-template-columns: 1fr;
    gap: 0.8rem;
  }
}
</style>
