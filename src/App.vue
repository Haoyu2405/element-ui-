<template>
  <div id="app">
    <!-- 卡片组件 -->
    <el-card class="login-card">
      <!-- 登录表单 -->
      <el-form
        style="margin-top: 50px"
        :model="loginForm"
        :rules="loginRules"
        ref="loginForm"
      >
        <el-form-item prop="mobile">
          <el-input
            placeholder="请输入手机号"
            v-model="loginForm.mobile"
          ></el-input>
        </el-form-item>
        <el-form-item prop="password">
          <el-input
            placeholder="请输入密码"
            v-model="loginForm.password"
          ></el-input>
        </el-form-item>
        <el-form-item>
          <el-button type="primary" style="width: 100%" @click="login"
            >登录</el-button
          >
        </el-form-item>
      </el-form>
    </el-card>
  </div>
</template>

<script>
export default {
  data() {
    // 自定义校验函数
    const checkMobile = (rule, value, callback) => {
      value.charAt(2) === '9'
        ? callback()
        : callback(new Error('第三位手机号必须为9'))
    }
    return {
      // 定义表单数据对象
      loginForm: {
        mobile: '',
        password: '',
      },

      // 校验规则
      loginRules: {
        // 校验的字段名
        mobile: [
          {
            required: true,
            message: '手机号不能为空',
            trigger: 'blur',
          },
          {
            pattern: /^1[3-9]\d{9}$/,
            message: '请输入正确的手机号',
            trigger: 'blur',
          },
          {
            trigger: 'blur',
            validator: checkMobile,
          },
        ],
        password: [
          {
            required: true,
            message: '密码不能为空',
            trigger: 'blur',
          },
          {
            min: 6,
            max: 16,
            message: '密码应为6-16位的长度',
            trigger: 'blur',
          },
        ],
      },
    }
  },
  methods: {
    login() {
      this.$refs.loginForm.validate((isOk) => {
        if (isOk) {
          console.log('检验通过') // 执行校验通过的业务
          return
        }
        console.log('校验失败')
      })
    },
  },
  components: {},
}
</script>

<style>
#app {
  width: 100%;
  height: 100vh;
  background-color: pink;
  display: flex;
  justify-content: center;
  align-items: center;
}
.login-card {
  width: 440px;
  height: 300px;
}
</style>
