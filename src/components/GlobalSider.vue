<template>
  <div id="globalSider">
    <a-layout-sider v-if="loginUserStore.loginUser.id"
                    class="sider"
                    width="200"
                    breakpoint="lg"
    >
      <a-menu v-model:selectedKeys="current" mode="inline" :items="items" @click="doMenuClick" />
    </a-layout-sider>

  </div>
</template>
<script lang="ts" setup>
import { computed, h, ref } from 'vue'
import { PictureOutlined, UserOutlined } from '@ant-design/icons-vue'
import { MenuProps } from 'ant-design-vue'
import { useRouter } from 'vue-router'
import { useLoginUserStore } from '@/stores/user.ts'

const loginUserStore = useLoginUserStore()
const router = useRouter()

// 当前选中菜单
const current = ref<string[]>([])
// 监听路由变化，更新当前选中菜单
router.afterEach((to, from, next) => {
  current.value = [to.path]
})
// 路由跳转事件
const doMenuClick = ({ key }: { key: string }) => {
  router.push({
    path: key,
  })
}


// 菜单列表
const menuItems = [
  {
    key: '/',
    icon: () => h(PictureOutlined),
    label: '公共图库',
    title: '公共图库',
  },
  {
    key: '/my_space',
    icon: () => h(UserOutlined),
    label: '我的空间',
    title: '我的空间',
  },

]


// 展示在菜单的路由数组
const items = computed<MenuProps['items']>(() => menuItems)
</script>

<style scoped>

</style>
