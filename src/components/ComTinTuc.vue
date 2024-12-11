<template>
  <div class="news-page">
    <div class="hero-section">
      <h2>Tin Tức Mới Nhất</h2>
      <p>Hãy theo dõi các bài viết về món ăn và xu hướng ẩm thực mới nhất!</p>
    </div>

    <div class="news-list">
      <div class="news-item" v-for="(news, index) in newsArticles" :key="index">
        <img :src="news.image" :alt="news.title" class="news-image" />
        <div class="news-content">
          <h3>{{ news.title }}</h3>
          <p class="news-description">{{ news.description }}</p>
          <p class="news-date">{{ news.date }}</p>
          <!-- Link đến trang chi tiết -->
          <router-link :to="{ name: 'news-detail', params: { id: news.id } }" class="read-more">Đọc thêm</router-link>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ComTinTuc',
  data() {
    return {
      newsArticles: [
        {
          id: '1',
          title: "Khám Phá Món Ăn Mới Của Tháng",
          description: "Tìm hiểu những món ăn mới lạ sẽ làm bạn bất ngờ trong tháng này.",
          date: "15 Tháng 11, 2024",
          image: require("@/assets/gioithieu.jpg"),
        },
        {
          id: '2',
          title: "Top 5 Món Ăn Hấp Dẫn Cho Mùa Đông",
          description: "Những món ăn ấm nóng lý tưởng cho mùa đông lạnh giá.",
          date: "12 Tháng 11, 2024",
          image: require("@/assets/an-6.jpg"),
        },
        {
          id: '3',
          title: "Cách Làm Món Ăn Đặc Sản Từ Hải Sản",
          description: "Hướng dẫn chế biến các món ăn ngon từ hải sản tươi ngon.",
          date: "10 Tháng 11, 2024",
          image: require("@/assets/images.jpg"),
        }
      ]
    }
  }
}
</script>

<style scoped>
.news-page {
  max-width: 1200px;
  margin: 20px auto;
  padding: 30px;
  background-color: #fff;
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.1);
}

.hero-section {
  text-align: center;
  margin-bottom: 40px;
}

.hero-section h2 {
  font-size: 36px;
  color: #f57c00;
  font-weight: bold;
}

.hero-section p {
  font-size: 18px;
  color: #555;
}

.news-list {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 30px;
  margin-top: 20px;
}

.news-item {
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  background-color: #f9f9f9;
  transition: transform 0.3s ease;
}

.news-item:hover {
  transform: scale(1.05);
}

.news-image {
  width: 100%;
  height: 200px;
  object-fit: cover;
}

.news-content {
  padding: 20px;
}

.news-content h3 {
  font-size: 24px;
  font-weight: bold;
  color: #333;
  margin-bottom: 15px;
}

.news-description {
  font-size: 16px;
  color: #777;
  margin-bottom: 15px;
}

.news-date {
  font-size: 14px;
  color: #f57c00;
  font-weight: bold;
}

.read-more {
  display: inline-block;
  margin-top: 10px;
  font-size: 16px;
  color: #f57c00;
  text-decoration: none;
  border: 2px solid #f57c00;
  padding: 8px 15px;
  border-radius: 20px;
  transition: background-color 0.3s ease;
}

.read-more:hover {
  background-color: #f57c00;
  color: white;
}
</style>
