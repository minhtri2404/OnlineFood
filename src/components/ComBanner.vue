<template>
    <div class="banner">
      <h2>Welcome to Our Restaurant</h2>
      <p>Discover the best dishes and enjoy your time</p>
    </div>
  </template>
  
  <script>
  export default {
    name: 'ComBanner'
  }
  </script>
  
  <style>
  .banner {
    background-image: url('@/assets/food_menu/buger.jpg'); /* Cập nhật đường dẫn hình ảnh tại đây */
    background-size: cover;
    background-position: center;
    height: 300px; /* Điều chỉnh chiều cao banner */
    color: white;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    text-align: center;
    padding: 20px;
  }
  
  .banner h2 {
    font-size: 36px;
    margin: 0;
  }
  
  .banner p {
    font-size: 18px;
    margin: 10px 0 0;
  }
  </style>
  