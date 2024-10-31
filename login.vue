/** *@description: *@author: YuChen Zhang *@date: 2024-06-05 */
<template>
  <div class="login">
    <div class="banner">
      <el-form ref="loginForm" :model="user" status-icon label-width="80px">
        <h3>登录</h3>
        <hr />
        <el-form-item prop="username" label="用户名">
          <el-input
            v-model="user.username"
            placeholder="请输入用户名"
            prefix-icon
          ></el-input>
        </el-form-item>
        <el-form-item id="password" prop="password" label="密码">
          <el-input
            v-model="user.password"
            show-password
            placeholder="请输入密码"
          ></el-input>
        </el-form-item>
        <el-form-item>
          <el-button type="primary" icon="el-icon-upload" @click="login"
            >登 录</el-button
          >
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      user: {
        username: "",
        password: "",
      },
    };
  },
  methods: {
    login() {
      if (this.user.username.trim() == "" && this.user.password.trim() == "") {
        this.$message({
          message: "用户名或者密码没有输入",
          type: "error",
        });
        return;
      }
      var that = this;
      axios
        .post(this.baseURL + "user/login", {
          userAccount: this.user.username,
          userPwd: this.user.password,
        })
        .then((res) => {
          console.log(res);
          var user = res.data.data.user;
          var tokens = res.data.data.authorization;
          sessionStorage.setItem("token", tokens);
          sessionStorage.setItem("userId", user.userId);
          this.$router.push("/");
          window.location.reload();
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
};
</script>

<style scoped>
.login {
  width: 100%;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  background: url("../assets/login-bg.gif");
}
.banner {
  width: 40%;
  height: 80%;
}
.banner span {
  display: flex;
  align-items: center;
  margin-bottom: 30px;
}
.banner span .el-input {
  width: 80%;
}
h3 {
  color: #45fffcb8;
  font-size: 24px;
}
hr {
  background-color: #83fff3;
  margin: 20px auto;
}

.el-button {
  width: 50%;
  margin-left: -50px;
}
</style>
<style>
.el-form-item__label {
  color: aquamarine;
}
</style>
