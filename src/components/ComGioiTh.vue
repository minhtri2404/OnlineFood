<template>
  <div class="about-page">
    <div class="hero-section">
      <h1>Chào mừng đến với Trang Giới Thiệu!</h1>
      <p>
        Chúng tôi mang đến những món ăn tuyệt vời nhất, được chế biến từ những nguyên liệu
        tươi ngon, phục vụ tận tâm đến từng khách hàng.
      </p>
    </div>
    <div class="content-section">
      <h2>Về Chúng Tôi</h2>
      <p>
        Chúng tôi tự hào là một trong những nhà hàng hàng đầu, chuyên cung cấp các món ăn Việt Nam truyền thống kết hợp với phong cách hiện đại. Với sứ mệnh "Lan tỏa hương vị Việt", chúng tôi không ngừng cải thiện chất lượng và dịch vụ để mang lại sự hài lòng tối đa cho khách hàng.
      </p>
      <div class="image-gallery">
        <img src="@/assets/gioithieu.jpg" alt="Image 1" />
        <img src="@/assets/an-6.jpg" alt="Image 2" />
        <img src="@/assets/images.jpg" alt="Image 3" />
      </div>
    </div>
    <div class="contact-section">
      <h2>Liên Hệ</h2>
      <p>📍 Địa chỉ: 123 Đường Nguyễn Văn Quá, Quận 12, TP. Hồ Chí Minh</p>
      <p>📞 Điện thoại: (0123) 456-789</p>
      <p>📧 Email: lienhe@monngonviet.com</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "ComGioiTh"
};
</script>

<style scoped>
/* Bố cục tổng thể */
.about-page {
  font-family: Arial, sans-serif;
  line-height: 1.6;
  color: #333;
  padding: 20px;
  background-color: #f9f9f9;
}

/* Phần tiêu đề chính */
.hero-section {
  text-align: center;
  padding: 50px 20px;
  background-color: #fcb034;
  color: white;
  border-radius: 10px;
}

.hero-section h1 {
  font-size: 48px;
  margin-bottom: 20px;
}

.hero-section p {
  font-size: 18px;
  margin: 0 auto;
  max-width: 800px;
}

/* Phần nội dung */
.content-section {
  margin: 40px 0;
  text-align: center;
}

.content-section h2 {
  font-size: 36px;
  margin-bottom: 20px;
  color: #fcb034;
}

.content-section p {
  max-width: 800px;
  margin: 0 auto;
  color: #555;
}

/* Thư viện ảnh */
.image-gallery {
  display: flex;
  gap: 20px;
  justify-content: center;
  margin-top: 20px;
}

.image-gallery img {
  width: 300px;
  height: 200px;
  border-radius: 10px;
  object-fit: cover;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s;
}

.image-gallery img:hover {
  transform: scale(1.05);
}

/* Phần liên hệ */
.contact-section {
  text-align: center;
  padding: 20px;
  background-color: #ffe198;
  border-radius: 10px;
}

.contact-section h2 {
  font-size: 36px;
  margin-bottom: 20px;
  color: #333;
}

.contact-section p {
  font-size: 18px;
  color: #555;
  margin: 5px 0;
}

/* Hiệu ứng chung */
h2,
h1 {
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
}
</style>
