<template>
  <el-container class="app-wrapper">
    <el-aside :width="asideWidth" class="sidebar-container">
      <Menu />
    </el-aside>
    <el-container
      class="container"
      :class="{ hidderContainer: !$store.getters.siderType }"
    >
      <el-header>
        <Headers />
      </el-header>
      <el-main>
        <router-view v-slot="{ Component }">
          <transition name="fade-transform" mode="out-in">
            <component :is="Component" />
          </transition>
        </router-view>
      </el-main>
    </el-container>
  </el-container>
</template>

<script setup>
import Menu from './Menu'
import Headers from './headers'
import { computed } from 'vue'
import variables from '@/styles/variables.scss'
import store from '@/store'

const asideWidth = computed(() => {
  return store.getters.siderType
    ? variables.sideBarWidth
    : variables.hideSideBarWidth
})
</script>

<style lang="scss" scoped>
.app-container {
  @include relative;
}

.container {
  width: calc(100% - $sideBarWidth);
  height: 100%;

  position: fixed;
  top: 0;
  right: 0;
  z-index: 9;
  transition: all 0.28s;

  &.hidderContainer {
    width: calc(100% - $hideSideBarWidth);
  }
}

::v-deep(.el-header) {
  padding: 0;
}
</style>
<style></style>
