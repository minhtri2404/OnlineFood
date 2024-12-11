<template>
  <div class="contact-page">
    <div class="hero-section">
      <h2>Liên Hệ Với Chúng Tôi</h2>
      <p>Chúng tôi rất vui khi nhận được ý kiến phản hồi từ bạn. Hãy để lại thông tin dưới đây và chúng tôi sẽ phản hồi sớm nhất có thể.</p>
    </div>
    
    <form @submit.prevent="submitForm">
      <div class="form-group">
        <label for="name">Họ và tên:</label>
        <input type="text" id="name" v-model="name" placeholder="Nhập họ và tên của bạn" required />
      </div>

      <div class="form-group">
        <label for="email">Email:</label>
        <input type="email" id="email" v-model="email" placeholder="Nhập email của bạn" required />
      </div>

      <div class="form-group">
        <label for="message">Lời nhắn:</label>
        <textarea id="message" v-model="message" rows="6" placeholder="Viết lời nhắn của bạn tại đây..." required></textarea>
      </div>

      <button type="submit">Gửi Lời Nhắn</button>
    </form>
  </div>
</template>

<script>
export default {
  name: 'ComLienHe',
  data() {
    return {
      name: '',
      email: '',
      message: ''
    }
  },
  methods: {
    submitForm() {
      // Xử lý logic khi gửi biểu mẫu
      alert(`Cảm ơn ${this.name} đã liên hệ! Chúng tôi sẽ phản hồi qua email: ${this.email}`);
      // Sau khi gửi, có thể đặt lại các trường nhập liệu
      this.name = '';
      this.email = '';
      this.message = '';
    }
  }
}
</script>

<style scoped>
.contact-page {
  max-width: 600px;
  margin: 20px auto;
  padding: 30px;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  background-color: #fff9e6;
  box-shadow: 0 6px 18px rgba(0, 0, 0, 0.1);
}

.hero-section {
  text-align: center;
  margin-bottom: 30px;
}

.hero-section h2 {
  font-size: 28px;
  color: #f57c00;
  font-weight: bold;
  margin-bottom: 10px;
}

.hero-section p {
  font-size: 16px;
  color: #555;
}

h2 {
  text-align: center;
  color: #333;
  margin-bottom: 20px;
}

.form-group {
  margin-bottom: 20px;
}

label {
  display: block;
  font-size: 16px;
  font-weight: bold;
  color: #333;
  margin-bottom: 8px;
}

input,
textarea {
  width: 100%;
  padding: 12px;
  border: 1px solid #ccc;
  border-radius: 5px;
  font-size: 16px;
  box-sizing: border-box;
  margin-top: 6px;
  transition: border 0.3s ease;
}

input:focus,
textarea:focus {
  border-color: #f57c00;
  outline: none;
}

button {
  width: 100%;
  padding: 12px;
  border: none;
  border-radius: 5px;
  background-color: #f57c00;
  color: white;
  font-size: 18px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #e65100;
}

button:active {
  background-color: #bf360c;
}

button:disabled {
  background-color: #ddd;
  cursor: not-allowed;
}
</style>
