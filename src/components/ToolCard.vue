<template>
  <a :href="tool.url" target="_blank" rel="noopener noreferrer" class="tool-card">
    <div class="tool-card__header">
      <h3 class="tool-card__name">{{ tool.name }}</h3>
      <span class="tool-card__external">↗</span>
    </div>
    <p class="tool-card__description">{{ tool.description }}</p>
    <div class="tool-card__tags">
      <span v-for="tag in tool.tags" :key="tag" class="tool-card__tag">#{{ tag }}</span>
    </div>
  </a>
</template>

<script setup>
defineProps({
  tool: {
    type: Object,
    required: true,
  },
});
</script>

<style scoped>
.tool-card {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  padding: 1.25rem;
  background: var(--color-card-bg);
  border: 1px solid var(--color-border);
  border-radius: 12px;
  text-decoration: none;
  color: inherit;
  transition: border-color 0.2s, box-shadow 0.2s, transform 0.15s;
}

.tool-card:hover {
  border-color: var(--color-accent);
  box-shadow: 0 4px 20px var(--color-shadow);
  transform: translateY(-2px);
}

.tool-card__header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 0.5rem;
}

.tool-card__name {
  font-size: 1rem;
  font-weight: 600;
  color: var(--color-text-primary);
  margin: 0;
}

.tool-card__external {
  font-size: 1rem;
  color: var(--color-text-muted);
  transition: color 0.2s;
}

.tool-card:hover .tool-card__external {
  color: var(--color-accent);
}

.tool-card__description {
  font-size: 0.875rem;
  line-height: 1.55;
  color: var(--color-text-secondary);
  margin: 0;
  flex: 1;
}

.tool-card__tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.375rem;
  margin-top: 0.25rem;
}

.tool-card__tag {
  font-size: 0.72rem;
  padding: 0.2rem 0.55rem;
  background: var(--color-tag-bg);
  color: var(--color-tag-text);
  border-radius: 999px;
  font-weight: 500;
}
</style>
