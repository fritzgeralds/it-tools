<script lang="ts" setup>
import { useStyleStore } from '@/stores/style.store';
import { IconBrandGithub, IconInfoCircle, IconMoon, IconSun } from '@tabler/icons-vue';

const styleStore = useStyleStore();
const { isDarkTheme } = toRefs(styleStore);
</script>

<template>
  <c-tooltip :tooltip="$t('home.nav.github')" position="bottom">
    <c-button
      :aria-label="$t('home.nav.githubRepository')"
      circle
      href="https://github.com/CorentinTh/it-tools"
      rel="noopener noreferrer"
      target="_blank"
      variant="text"
    >
      <n-icon :component="IconBrandGithub" size="25" />
    </c-button>
  </c-tooltip>

  <c-tooltip :tooltip="$t('home.nav.about')" position="bottom">
    <c-button :aria-label="$t('home.nav.aboutLabel')" circle to="/about" variant="text">
      <n-icon :component="IconInfoCircle" size="25" />
    </c-button>
  </c-tooltip>
  <c-tooltip :tooltip="isDarkTheme ? $t('home.nav.lightMode') : $t('home.nav.darkMode')" position="bottom">
    <c-button :aria-label="$t('home.nav.mode')" circle variant="text" @click="() => styleStore.toggleDark()">
      <n-icon v-if="isDarkTheme" :component="IconSun" size="25" />
      <n-icon v-else :component="IconMoon" size="25" />
    </c-button>
  </c-tooltip>
</template>

<style lang="less" scoped>
.n-button {
  &:not(:last-child) {
    margin-right: 5px;
  }
}
</style>
