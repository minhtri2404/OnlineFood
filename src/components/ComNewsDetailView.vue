<template>
    <div class="news-detail">
      <div class="news-hero">
        <h1>{{ news.title }}</h1>
        <p class="news-date">{{ news.date }}</p>
      </div>
      <img :src="news.image" alt="news image" class="news-image" />
      <div class="news-description">
        <p>{{ news.description }}</p>
        <p v-if="news.content">{{ news.content }}</p>
      </div>
      <a href="/news" class="back-link">Quay lại danh sách tin tức</a>
    </div>
  </template>
  
  <script>
  export default {
    name: 'NewsDetailView',
    data() {
      return {
        news: {}  // Chứa thông tin chi tiết bài viết
      };
    },
    mounted() {
      // Lấy id từ URL để hiển thị bài viết tương ứng
      const newsId = this.$route.params.id;
      // Giả sử bạn có một nguồn dữ liệu tin tức
      const newsArticles = [
        {
          id: '1',
          title: 'Khám Phá Món Ăn Mới Của Tháng',
          description: 'Tìm hiểu những món ăn mới lạ sẽ làm bạn bất ngờ trong tháng này.',
          date: '15 Tháng 11, 2024',
          image: require("@/assets/gioithieu.jpg"),
          content: 'Chi tiết về món ăn mới...'
        },
        {
          id: '2',
          title: 'Top 5 Món Ăn Hấp Dẫn Cho Mùa Đông',
          description: 'Những món ăn ấm nóng lý tưởng cho mùa đông lạnh giá.',
          date: '12 Tháng 11, 2024',
          image: require("@/assets/an-6.jpg"),
          content: 'Thông tin chi tiết về các món ăn mùa đông.'
        },
        {
          id: '3',
          title: "Cách Làm Món Ăn Đặc Sản Từ Hải Sản",
          description: "Hướng dẫn chế biến các món ăn ngon từ hải sản tươi ngon.",
          date: "10 Tháng 11, 2024",
          image: require("@/assets/images.jpg"),
        }
        // Thêm các bài viết khác ở đây
      ];
  
      // Tìm bài viết theo id
      this.news = newsArticles.find(article => article.id === newsId);
    },
  }
  </script>
  
  <style scoped>
  .news-detail {
    max-width: 1000px;
    margin: 40px auto;
    padding: 20px;
    background-color: #fff;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  }
  
  .news-hero {
    text-align: center;
  }
  
  .news-hero h1 {
    font-size: 36px;
    color: #f57c00;
    font-weight: bold;
  }
  
  .news-date {
    font-size: 16px;
    color: #f57c00;
  }
  
  .news-image {
    width: 100%;
    height: 300px;
    object-fit: cover;
    margin-top: 20px;
  }
  
  .news-description {
    margin-top: 20px;
    font-size: 18px;
    color: #555;
  }
  
  .back-link {
    display: inline-block;
    margin-top: 20px;
    color: #f57c00;
    text-decoration: none;
    border: 2px solid #f57c00;
    padding: 10px 20px;
    border-radius: 20px;
  }
  
  .back-link:hover {
    background-color: #f57c00;
    color: white;
  }
  </style>
  