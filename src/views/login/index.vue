<template>
  <div class="login_container">
    <el-row>
      <el-col :span="12" :xs="0"></el-col>
      <el-col :span="12" :xs="24">
        <el-form class="login_form" :model="loginForm" :rules="rules">
          <h1>HELLO</h1>
          <h2>欢迎来到虎子甄选</h2>
          <el-form-item prop="username">
            <el-input :prefix-icon="User" v-model="loginForm.username"/>
          </el-form-item>
          <el-form-item prop="password">
            <el-input :prefix-icon="Lock" type="password" v-model="loginForm.password" show-password />
          </el-form-item>
          <el-form-item>
            <el-button :loading="loading" type="primary" class="login_btn" @click="login">登录</el-button>
          </el-form-item>

        </el-form>
      </el-col>
    </el-row>
  </div>
</template>

<script lang="ts" setup>
import {User,Lock,View}  from "@element-plus/icons-vue";
import {reactive, ref} from "vue";
import useUserStore from "@/store/modules/user";
import {useRouter} from "vue-router";
import {ElNotification} from "element-plus";
import {getTime} from "@/utils/times";

let $router = useRouter();
let loginForm = reactive({username:'',password:''});
let useStore = useUserStore();
let loading = ref(false)
const login = async ()=>{
  loading.value = true;
  try {
    await useStore.userLogin(loginForm);
    $router.push('/');
    ElNotification({
      type:"success",
      message:"欢迎回来",
      title:`Hi!,${getTime()}好`
    })
    loading.value = false;
  }catch (error){
    loading.value = false;
    ElNotification({
      type:"error",
      message:(error as Error).message
    })
  }
}
const rules = {
  username:[
    {required:true,message: '用户名不能为空',trigger:'change'},
    {min:6,max:10,message: '账号长度至少六位',trigger: 'change'}
  ],
  password:[
    {required:true,min:6,max:15,message:'密码长度至少六位',trigger:'change'}
  ]
}
</script>

<style scoped lang="scss">
.login_container{
  width: 100%;
  height: 100vh;
  background:url("@/assets/images/background.jpg") no-repeat;
  background-size: cover;
  .login_form{
    position: relative;
    width: 80%;
    top: 30vh;
    background: url("@/assets/images/login_form.png") no-repeat;
    background-size: cover;
    padding: 40px;
    h1{
      color: white;
      font-size: 40px;
    }
    h2{
      font-size: 20px;
      color: white;
      margin: 20px 0px;
    }
    .login_btn {
      width: 100%;
    }
  }
}
</style>