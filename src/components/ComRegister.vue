<template>
  <div>
    <h2>Đăng ký tài khoản</h2>
    <p v-if="error" class="error">{{ error }}</p>
    <input v-model="username" placeholder="Tên đăng nhập" required />
    <input v-model="password" type="password" placeholder="Mật khẩu" required />
    <input v-model="confirmPassword" type="password" placeholder="Xác nhận mật khẩu" required />
    <button @click="register">Đăng ký</button>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      username: "",
      password: "",
      confirmPassword: "",
      error: "",
    };
  },
  methods: {
    async register() {
      // Kiểm tra xem mật khẩu và xác nhận mật khẩu có trùng khớp không
      if (this.password !== this.confirmPassword) {
        this.error = "Mật khẩu không trùng";
        return;
      }

      try {
        // Kiểm tra xem tên người dùng đã tồn tại trong JSON Server chưa
        const { data: existingUsers } = await axios.get(
          "http://localhost:3000/users"
        );

        const userExists = existingUsers.find(
          (user) => user.username === this.username
        );

        if (userExists) {
          this.error = "Tên đăng nhập đã tồn tại";
          return;
        }

        // Tạo người dùng mới
        const newUser = {
          username: this.username,
          password: this.password,
        };

        // Gửi dữ liệu tới JSON Server
        await axios.post("http://localhost:3000/users", newUser);

        alert("Đăng ký thành công!");
        this.error = "";

        // Xóa dữ liệu trên form
        this.username = "";
        this.password = "";
        this.confirmPassword = "";

        // Điều hướng tới trang đăng nhập
        this.$router.push("/login");
      } catch (error) {
        console.error("Đã xảy ra lỗi khi đăng ký:", error);
        this.error = "Đã xảy ra lỗi. Vui lòng thử lại sau.";
      }
    },
  },
};
</script>

<style scoped>
div {
  max-width: 400px;
  margin: 20px auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 8px;
  background-color: #f9f9f9;
}

h2 {
  text-align: center;
  font-size: 24px;
  margin-bottom: 20px;
}

input {
  width: 95%;
  padding: 10px;
  margin: 10px 0;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 16px;
}

button {
  width: 100%;
  padding: 10px;
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 4px;
  font-size: 16px;
  cursor: pointer;
}

button:hover {
  background-color: #45a049;
}

.error {
  color: red;
  font-size: 14px;
  text-align: center;
  margin-top: 10px;
}
</style>
