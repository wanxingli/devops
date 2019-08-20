<template>
  <a-layout id="components-layout-demo-top-side-2">
    <SideMenu
      mode="inline"
      :menus="menus"
      @menuSelect="menuSelect"
      :theme="navTheme"
      :collapsed="false"
      :collapsible="true"
    ></SideMenu>
    <a-layout style="padding: 0 24px 24px">
      <a-layout-content :style="{ background: '#fff', padding: '24px', margin: 0, minHeight: '280px' }">
       project
      </a-layout-content>
    </a-layout>
  </a-layout>
</template>

<script>
  import SideMenu from '@/components/menu/SideMenu'
  import { mixin, mixinDevice } from '@/utils/mixin.js'
  import { mapState, mapActions } from 'vuex'

  export default {
    name: "Analysis",
    components: {
      SideMenu
    },
    mixins: [mixin, mixinDevice],
    computed: {
      ...mapState({
        // 主路由
        mainRouters: state => state.permission.addRouters,
        // 后台菜单
        permissionMenuList: state => state.user.permissionList
      })
    },
    data() {
      return {
        menus: [],
        size: 'project',
      }
    },
    created() {
      this.menus = this.permissionMenuList
      // this.menus.push(this.permissionMenuList[0])
    },
    methods: {
      // ...mapActions(['setHomeProjectId', 'getProjectList']),

    }
  }
</script>

<style lang="scss" scoped>

</style>