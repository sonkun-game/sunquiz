<template>
  <div class="container">
    <div class="login-box bg-yellow-50 border-teddy-brow">
      <div class="bg-teddy-brow w-full p-4">
        <p class="text-xl">Student Login</p>
      </div>
      <div class="login-input flex">
        <div class="m-auto">
          <div class="py-1">
            <label for="user">User :</label>
            <input v-model="username" id="user" name="user" type="text" />
          </div>
          <div class="py-1">
            <label for="user">Pass :</label>
            <input v-model="password" id="pass" name="pass" type="password" />
          </div>
          <div class="py-1 flex justify-end">
            <button @click="loginForm()" style="width: 100px;" class="bg-teddy-brow rounded-lg bold p-2 w-full">
              <i class="fa-solid fa-hammer text-white"></i>
              <span class="text-white">Login</span>
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.container {
  height: 90vh;
}

.login-box {
  width: 500px;
  height: 300px;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}

.login-input {
  height: 200px;
}
</style>

<script>
import axios from 'axios'

export default {
  name: "LoginPage",
  layout: "welcome",
  data() {
        return {
            username: "",
            password: ""
        }
    },
  methods: {
        loginForm() {
            axios({
                method: 'post',
                url: 'http://127.0.0.1:8000/student/login',
                responseType: 'json',
                data: {
                  user_name: this.username,
                  password: this.password,
                }
            }).then( response => {
                var respData = response.data;
                console.log(respData);
                localStorage.setItem("user",respData.user_name);
                localStorage.setItem("fullName",respData.full_name);
                localStorage.setItem("token",respData.token);
                alert("Login thành công, chuyển hướng đến trang exam");
                this.$router.push('/exam');
            });
        }
    }
}
</script>