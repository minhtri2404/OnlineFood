<template>
  <div>
    <h2>Đăng nhập</h2>
    <p v-if="error" class="error">{{ error }}</p>
    <input v-model="username" placeholder="Tên đăng nhập" />
    <input v-model="password" type="password" placeholder="Mật khẩu" />
    <button @click="login">Đăng nhập</button>
  </div>
</template>

<script>
import axios from 'axios';  // Import axios
import eventBus from '@/eventBus';

export default {
  data() {
    return {
      username: '', // an
      password: '', // 1234
      error: '',
    };
  },
  methods: {
    async login() {
      try {
        // Gửi yêu cầu GET để tìm người dùng có tên đăng nhập và mật khẩu
        const response = await axios.get('http://localhost:3000/users', {
          params: {
            username: this.username,
            password: this.password,
          },
        });

        // Kiểm tra nếu có người dùng với thông tin đã nhập
        if (response.data.length > 0) {
          const user = response.data[0]; // Giả sử chỉ có một người dùng khớp
          // Lưu vào localStorage
          localStorage.setItem('currentuser', JSON.stringify(user));
          eventBus.emit('loginSuccess', user);
          this.$router.push('/');
        } else {
          this.error = 'Đăng nhập không thành công';
        }
      } catch (error) {
        this.error = 'Đã xảy ra lỗi khi đăng nhập';
        console.error(error);
      }
    },
  },
};
</script>

<style scoped>
.error {
  color: red;
  font-size: 14px;
  text-align: center;
  margin-top: 10px;
}

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
