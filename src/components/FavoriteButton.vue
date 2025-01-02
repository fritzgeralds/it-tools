<script lang="ts" setup>
import { useToolStore } from '@/tools/tools.store';
import type { Tool } from '@/tools/tools.types';

const props = defineProps<{ tool: Tool }>();

const toolStore = useToolStore();

const { tool } = toRefs(props);

const isFavorite = computed(() => toolStore.isToolFavorite({ tool }));
const buttonType = computed(() => (isFavorite.value ? 'primary' : 'default'));

function toggleFavorite(event: MouseEvent) {
  event.preventDefault();

  if (toolStore.isToolFavorite({ tool })) {
    toolStore.removeToolFromFavorites({ tool });
    return;
  }

  toolStore.addToolToFavorites({ tool });
}
</script>

<template>
  <c-tooltip :tooltip="isFavorite ? $t('favoriteButton.remove') : $t('favoriteButton.add')">
    <c-button
      :style="{ color: isFavorite ? '#d03050' : '#484848', opacity: isFavorite ? 1 : 0.2 }"
      :type="buttonType"
      circle
      variant="text"
      @click="toggleFavorite"
    >
      <icon-mdi-heart />
    </c-button>
  </c-tooltip>
</template>
