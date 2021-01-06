<template>
  <div class="login_container">
    <div class="login_box">
      <div>
        <!-- 登录区域 -->
        <el-form
          label-width="0px"
          class="login-form"
          :model="loginForm"
          :rules="loginFormRules"
          ref="loginFormRef"
        >
          <!-- 用户名 -->
          <el-form-item prop="username">
            <el-input
              prefix-icon="iconfont icon-user"
              v-model="loginForm.username"
              placeholder="用户名"
            ></el-input>
          </el-form-item>
          <!-- 密码 -->
          <el-form-item prop="password">
            <el-input
              prefix-icon="iconfont icon-3702mima"
              v-model="loginForm.password"
              placeholder="密码"
              type="password"
            ></el-input>
          </el-form-item>
          <!-- 按钮 -->
          <el-form-item class="btns">
            <el-button
            type="primary"
            @click="login">登录</el-button>
            <el-button
            type="info"
            @click="resetLoginForm">重置</el-button>
          </el-form-item>
        </el-form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      //初始化表单数据
      loginForm: {
        username: "",
        password: "",
      },
      loginFormRules: {
        username: [
          {
            required: true,
            message: "请输入登录名称",
            trigger: "blur",
          },
          {
            min: 3,
            max: 10,
            message: "长度在3到10个字符",
            trigger: "blur",
          },
        ],
        password: [
          {
            required: true,
            message: "请输入密码",
            trigger: "blur",
          },
          {
            min: 6,
            max: 15,
            message: "长度在6到15个字符",
            trigger: "blur",
          },
        ],
      },
    };
  },
  methods:{
    resetLoginForm() {
      this.$refs.loginFormRef.resetFields();
    },
    login() {
      this.$refs.loginFormRef.validate((valid) => {
        if(!valid)return;
        this.$http.post('login',this.loginForm)
      });
    }
  }
};
</script>

<style>
.login_container {
  width: 100vw;
  height: 100vh;
  background-color: dimgrey;
  display: flex;
  justify-content: center;
  align-items: center;
}
.login_box {
  position: relative;
  width: 33vw;
  height: 300px;
  background-color: #fff;
}
.login-form {
  position: absolute;
  bottom: 0;
  width: 100%;
  padding: 0 20px;
}
.btns {
  display: flex;
  justify-content: flex-end;
}
</style>
