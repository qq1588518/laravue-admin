<template>
  <div class='menu-wrapper'>
    <template v-for="item in routes">

      <router-link v-if="!item.hidden && item.noDropdown && item.children.length > 0" :to="item.children[0].path">
        <el-menu-item :index="item.children[0].path" class='submenu-title-noDropdown'>
          <i :class='`fa fa-${item.icon}`' aria-hidden="true"></i><span> {{ item.children[0].name }}</span>
        </el-menu-item>
      </router-link>

      <el-submenu :index="item.name" v-if="!item.noDropdown && !item.hidden">
        <template slot="title">
          <i :class='`fa fa-${item.icon}`' aria-hidden="true"></i><span> {{ item.name }}</span>
        </template>
        <template v-for="child in item.children" v-if='!child.hidden'>

          <sidebar-item class='nest-menu' v-if='child.children && child.children.length > 0' :routes='[child]'></sidebar-item>

          <router-link v-else :to="child.path">
            <el-menu-item :index="child.path">
              {{ child.name }}</span>
            </el-menu-item>
          </router-link>

        </template>

      </el-submenu>

    </template>
  </div>
</template>

<script>
export default {
  name: 'SidebarItem',
  props: {
    routes: {
      type: Array
    }
  }
}
</script>
