<template>
  <template v-for="subItem in menuList" :key="subItem.name">
    <el-sub-menu v-if="subItem.children?.length" :index="subItem.name">
      <template #title>
        <el-icon>
          <component :is="subItem.meta.icon ? subItem.meta.icon : 'HomeFilled'"></component>
        </el-icon>
        <span class="sle">{{ subItem.meta.title }}</span>
      </template>
      <SubMenu :menu-list="subItem.children" />
    </el-sub-menu>
    <el-menu-item v-else :index="subItem.path" @click="handleClickMenu(subItem)">
      <el-icon>
        <component :is="subItem.meta.icon ? subItem.meta.icon : 'Menu'"></component>
      </el-icon>
      <template #title>
        <span class="sle">{{ subItem.meta.title }}</span>
      </template>
    </el-menu-item>
  </template>
</template>

<script setup lang="ts">
import { useRouter } from "vue-router";

defineProps<{ menuList: Menu.MenuOptions[] }>();

const router = useRouter();
const handleClickMenu = (subItem: Menu.MenuOptions) => {
  if (subItem.meta.isLink) return window.open(subItem.meta.isLink, "_blank");
  router.push(subItem.path);
};
</script>

<style lang="scss">
/* flex */
.flx-center {
  display: flex;
  align-items: center;
  justify-content: center;
}

.flx-justify-between {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.flx-align-center {
  display: flex;
  align-items: center;
}

.el-sub-menu .el-sub-menu__title:hover {
  color: var(--el-menu-hover-text-color) !important;
  background-color: transparent !important;
}

.el-menu--collapse {
  .is-active {
    .el-sub-menu__title {
      color: #ffffff !important;
      background-color: var(--el-color-primary) !important;
    }
  }
}

.el-menu-item {
  &:hover {
    color: var(--el-menu-hover-text-color);
  }

  &.is-active {
    color: #409eff !important;
    background-color: #ecf5ff !important;

    &::before {
      position: absolute;
      top: 0;
      bottom: 0;
      width: 4px;
      content: "";
      background-color: var(--el-color-primary);
    }
  }
}

.vertical,
.classic,
.transverse {
  .el-menu-item {
    &.is-active {
      &::before {
        left: 0;
      }
    }
  }
}

.columns {
  .el-menu-item {
    &.is-active {
      &::before {
        right: 0;
      }
    }
  }
}

.classic,
.transverse {
  #driver-highlighted-element-stage {
    background-color: #606266 !important;
  }
}
</style>
