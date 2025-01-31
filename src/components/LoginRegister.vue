<template>
    <div class="login-register-container">
      <n-card title="登录或注册" style="max-width: 400px; margin: auto; padding: 20px;">
        <n-tabs v-model:value="activeTab">
          <n-tab-pane name="login" tab="登录">
            <n-form @submit.prevent="handleLogin">
              <n-form-item label="用户名">
                <n-input v-model="loginForm.username" placeholder="请输入用户名" />
              </n-form-item>
              <n-form-item label="密码">
                <n-input v-model="loginForm.password" type="password" placeholder="请输入密码" />
              </n-form-item>
              <n-button type="primary" block @click="handleLogin">登录</n-button>
            </n-form>
          </n-tab-pane>
          <n-tab-pane name="register" tab="注册">
            <n-form @submit.prevent="handleRegister">
              <n-form-item label="用户名">
                <n-input v-model="registerForm.username" placeholder="请输入用户名" />
              </n-form-item>
              <n-form-item label="密码">
                <n-input v-model="registerForm.password" type="password" placeholder="请输入密码" />
              </n-form-item>
              <n-form-item label="确认密码">
                <n-input v-model="registerForm.confirmPassword" type="password" placeholder="请确认密码" />
              </n-form-item>
              <n-button type="primary" block @click="handleRegister">注册</n-button>
            </n-form>
          </n-tab-pane>
        </n-tabs>
      </n-card>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  import { useMessage } from 'naive-ui';
  
  const activeTab = ref('login');
  const loginForm = ref({
    username: '',
    password: ''
  });
  const registerForm = ref({
    username: '',
    password: '',
    confirmPassword: ''
  });
  const message = useMessage();
  
  const handleLogin = () => {
    if (loginForm.value.username && loginForm.value.password) {
      message.success('登录成功！');
    } else {
      message.error('请填写所有字段！');
    }
  };
  
  const handleRegister = () => {
    if (
      registerForm.value.username &&
      registerForm.value.password &&
      registerForm.value.confirmPassword
    ) {
      if (registerForm.value.password === registerForm.value.confirmPassword) {
        message.success('注册成功！');
      } else {
        message.error('密码和确认密码不一致！');
      }
    } else {
      message.error('请填写所有字段！');
    }
  };
  </script>
  
  <style>
  .login-register-container {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    background-color: #f5f5f5;
  }
  </style>
  