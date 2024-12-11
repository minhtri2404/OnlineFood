<template>
  <footer>
    <div class="footer-container">
      <div class="footer-column">
        <h3>Popular Dishes</h3>
        <ul>
          <li><a href="#">Appetizers</a></li>
          <li><a href="#">Soups</a></li>
          <li><a href="#">Main Course</a></li>
          <li><a href="#">Desserts</a></li>
          <li><a href="#">Beverages</a></li>
        </ul>
      </div>
      <div class="footer-column">
        <h3>Our Specials</h3>
        <ul>
          <li><a href="#">Chef's Specials</a></li>
          <li><a href="#">Seasonal Dishes</a></li>
          <li><a href="#" class="highlight">Best Sellers</a></li>
          <li><a href="#">Healthy Choices</a></li>
          <li><a href="#">New Arrivals</a></li>
        </ul>
      </div>
      <div class="footer-column">
        <h3>About Us</h3>
        <ul>
          <li><a href="#">Our Story</a></li>
          <li><a href="#">Meet the Chef</a></li>
          <li><a href="#">Customer Reviews</a></li>
          <li><a href="#">Blog</a></li>
          <li><a href="#">Gallery</a></li>
        </ul>
      </div>
      <div class="footer-column">
        <h3>Contact</h3>
        <ul class="contact-info">
          <li><span>📍</span> 123 Đường Nguyễn Văn Quá, Quận 12, TP. Hồ Chí Minh</li>
          <li><span>📞</span> (0123) 456-789</li>
          <li><span>✉️</span> Email: lienhe@monngonviet.com</li>
        </ul>
      </div>
    </div>
    
    <!-- Thêm phần bản đồ vào đây -->
    <div class="map-container">
      <iframe 
        src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3151.8354345093743!2d144.9537353154077!3d-37.81720974202125!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x6ad65d43f5a2b9b5%3A0x5045675218ce7e33!2zU29tZSBQbGFjZSwgTWVsYm91cm5lLCBBdXN0cmFsaWE!5e0!3m2!1sen!2s!4v1614290570325!5m2!1sen!2s" 
        width="100%" 
        height="200" 
        style="border:0;" 
        allowfullscreen
        loading="lazy">
      </iframe>
    </div>
    
    <div class="footer-bottom">
      <div class="payment-icons">
        <img src="@/assets/visa.png" alt="Visa">
        <img src="@/assets/card.png" alt="MasterCard">
        <img src="@/assets/paypal.png" alt="PayPal">
        <!-- Thêm các icon thanh toán khác nếu cần -->
      </div>
      <p>© 2024 FoodPlace. All Rights Reserved.</p>
    </div>
  </footer>
</template>

<style>
footer {
  background-color: #1e1e1e;
  color: #ffffff;
  padding: 50px 20px;
  font-family: Arial, sans-serif;
}

.footer-container {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
  max-width: 1200px;
  margin: 0 auto;
}

.footer-column {
  flex: 1;
  min-width: 200px;
  margin: 10px;
}

.footer-column h3 {
  color: #ff7043;
  font-size: 16px;
  text-transform: uppercase;
  position: relative;
  display: inline-block; /* Để gạch ngang nằm ngay dưới chữ */
  margin-bottom: 20px;
}

.footer-column h3::after {
  content: "";
  display: block;
  width: 30px;
  height: 2px;
  background-color: #ff7043;
  margin-top: 5px;
  position: absolute;
  bottom: -5px; /* Điều chỉnh để gạch ngang nằm ngay dưới chữ */
  left: 0;
}

.footer-column ul {
  list-style: none;
  padding: 0;
}

.footer-column li {
  margin-bottom: 10px;
}

.footer-column a {
  color: #b3b3b3;
  text-decoration: none;
  transition: color 0.3s ease;
}

.footer-column a:hover, .footer-column a.highlight {
  color: #ff7043;
}

.contact-info li {
  display: flex;
  align-items: center;
  color: #b3b3b3;
}

.contact-info span {
  margin-right: 8px;
  font-size: 18px;
}

.map-container {
  margin: 20px auto;
  max-width: 800px;
}

footer .footer-bottom {
  text-align: center;
  border-top: 1px solid #333;
  padding-top: 20px;
  margin-top: 20px;
  color: #b3b3b3;
  font-size: 14px;
}

.payment-icons img {
  width: 40px;
  margin: 0 10px;
  vertical-align: middle;
}
</style>
