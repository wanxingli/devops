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
            <div class="home_content_header">
              <a-radio-group :value="size" @change="handleSizeChange">
                <a-radio-button value="project">项目</a-radio-button>
                <a-radio-button value="projectGroup">项目群</a-radio-button>
              </a-radio-group>
            </div>
            <div class="home_content">
              <div class="project_card">
                <div class="card_header">
                  <div class="header-left">
                    <a-icon type="slack" class="iconfont_card" />
                    <span>D - 软件研发类</span>
                  </div>
                  <div class="header-right">
                    <span>活跃</span>
                  </div>
                </div>
                <div class="card_content">
                  <p>CMDB</p>
                  <p @click="enterProject">cmdb</p>
                </div>
              </div>
            </div>
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
      // this.menus = this.permissionMenuList
      this.menus.push(this.permissionMenuList[0])
    },
    methods: {
      // ...mapActions(['setHomeProjectId', 'getProjectList']),
      menuSelect() {
        if (!this.isDesktop()) {
          this.collapsed = false
        }
      },
      handleSizeChange (e) {
        this.size = e.target.value
      },
      enterProject () {
        // this.setHomeProjectId(111111)
        this.$router.push({name: 'project'})
      }
    }
  }
</script>

<style lang="scss" scoped>
.home_content_header {
  margin-bottom: 20px;
}
.home_content {
  width: 100%;
  display: flex;
  flex-wrap: wrap;
  .project_card {
    width: 360px;
    height: 200px;
    border-radius: 6px;
    overflow: hidden;
    background: #778899;
    margin: 0 20px 20px 0;
    .card_header {
      height: 50px;
      border-bottom: 1px solid #fff;
      color: #fff;
      font: 16px/50px '';
      display: flex;
      justify-content: space-between;
      justify-items: center;
      padding: 0 20px;
      .header-left {
        .iconfont_card {
          font-size: 28px;
          vertical-align: middle;
          margin: -3px 8px 0 0;
        }
      }
    }
    .card_content {
      padding: 20px;
      p {
        color: #fff;
        margin: 0;
        &:first-child {
          font: 18px/36px '';
          margin-bottom: 14px;
        }
        &:last-child {
          font: 800 28px/28px '';
          cursor: pointer;
        }
      }
    }
  }
}
</style>