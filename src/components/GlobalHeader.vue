<template>
  <nav class="navbar navbar-dark bg-primary justify-content-between mb-4 px-4">
    <router-link to="/" class="navbar-brand">月下论坛</router-link>
    <ul v-if="!user.isLogin" class="list-inline mb-0">
      <li class="list-inline-item"><router-link to="login" class="btn btn-outline-light my-2">登陆</router-link></li>
      <li class="list-inline-item"><router-link to="regist" href="#" class="btn btn-outline-light my-2">注册</router-link></li>
    </ul>
    <ul v-else class="list-inline mb-0">
      <li class="list-inline-item">
        <dropdown :title="`你好，${user.name}`">
          <dropdownitem><a href="#" class="dropdown-item" @click="toCreatePage">新建文章</a></dropdownitem>
          <dropdownitem disabled><a href="#" class="dropdown-item" @click="toedituser">我的资料</a></dropdownitem>
          <dropdownitem><a href="#" class="dropdown-item" @click="exitLogin">退出登录</a></dropdownitem>
        </dropdown>
      </li>
    </ul>
  </nav>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue'
import { useRouter } from 'vue-router'
import Dropdown from './DropDown.vue'
import Dropdownitem from './DropDownitem.vue'
import store, { UserProps } from '../store'

export default defineComponent({
  name: 'GlobalHeader',
  components: {
    Dropdown,
    Dropdownitem
  },
  props: {
    user: {
      type: Object as PropType<UserProps>,
      required: true
    }
  },
  setup () {
    const router = useRouter()
    const toCreatePage = () => {
      router.push('/createpage')
    }
    const exitLogin = () => {
      store.state.user.isLogin = false
      localStorage.setItem('isLogin', 'false')
      router.push('/')
    }
    const toedituser = () => {
      router.push('/edituser')
    }
    return {
      toCreatePage, exitLogin, toedituser
    }
  }
})
</script>
