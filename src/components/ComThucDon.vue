<template>
  <div class="menu-page">
    <h2>Thực Đơn Hôm Nay</h2>
    <div class="menu-items">
      <div class="menu-item" v-for="item in paginatedItems" :key="item.id">
        <img :src="item.image" :alt="item.name" class="menu-image" />
        <div class="menu-info">
          <h3>{{ item.name }}</h3>
          <p>{{ item.description }}</p>
          <p class="price">{{ item.price }} VND</p>
          <button @click="addToCart(item)" class="add-to-cart-btn">Thêm vào giỏ</button>
        </div>
      </div>
    </div>

    <!-- Phân trang -->
    <div class="pagination">
      <button @click="prevPage" :disabled="currentPage === 1">Trước</button>
      <button v-for="page in totalPages" :key="page" @click="goToPage(page)" :class="{ active: currentPage === page }">
        {{ page }}
      </button>
      <button @click="nextPage" :disabled="currentPage === totalPages">Tiếp</button>
    </div>
  </div>
</template>


<script>
import menus from '../data/items';
import cart from "@/data/cart";
import users from '@/data/users'

export default {
  name: 'ComThucDon',
  data() {
    return {
      menuItems: menus,
      cart: cart,
      currentPage: 1,
      itemsPerPage: 3,
      users: users,
      loggedInUser: null
    };
  },
  mounted() {
    this.loggedInUser = JSON.parse(localStorage.getItem('currentuser')) || null;
  },
  computed: {
    isUserLoggedIn() {
      return this.loggedInUser !== null;
    },
    totalPages() {
      return Math.ceil(this.menuItems.length / this.itemsPerPage);
    },
    paginatedItems() {
      const start = (this.currentPage - 1) * this.itemsPerPage;
      const end = start + this.itemsPerPage;
      return this.menuItems.slice(start, end);
    }
  },
  methods: {
    addToCart(item) {
      if (!this.isUserLoggedIn) {
        alert('Bạn cần đăng nhập để thêm sản phẩm vào giỏ hàng.');
        return;
      }

      const cartItem = this.cart.find(cartItem => cartItem.id === item.id);
      if (cartItem) {
        if (item.stock > 0) {
          cartItem.quantity += 1;
        }
      } else {
        if (item.stock > 0) {
          this.cart.push({ ...item, quantity: 1 });
        }
      }
      item.stock--;
      localStorage.setItem('cart', JSON.stringify(this.cart));
    },

    login(userId) {
      this.loggedInUser = this.users.find(user => user.id === userId);
      localStorage.setItem('currentuser', JSON.stringify(this.loggedInUser));
    },

    nextPage() {
      if (this.currentPage < this.totalPages) {
        this.currentPage++;
      }
    },
    prevPage() {
      if (this.currentPage > 1) {
        this.currentPage--;
      }
    },
    goToPage(page) {
      if (page >= 1 && page <= this.totalPages) {
        this.currentPage = page;
      }
    }
  }
};

</script>

<style scoped>
.menu-page {
  text-align: center;
  padding: 40px;
  background-color: #fafafa;
}

h2 {
  font-size: 36px;
  color: #333;
  margin-bottom: 20px;
}

.menu-items {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  justify-content: center;
}

.menu-item {
  width: 300px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  border-radius: 10px;
  overflow: hidden;
  background-color: #fff;
  transition: transform 0.3s;
}

.menu-item:hover {
  transform: scale(1.05);
}

.menu-image {
  width: 100%;
  height: 200px;
  object-fit: cover;
}

.menu-info {
  padding: 20px;
}

.menu-info h3 {
  font-size: 24px;
  color: #333;
}

.menu-info p {
  margin: 10px 0;
  color: #777;
}

.price {
  font-weight: bold;
  color: #fcb034;
}

.add-to-cart-btn {
  margin-top: 10px;
  padding: 10px 20px;
  background-color: #fcb034;
  color: #fff;
  border: none;
  border-radius: 20px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.add-to-cart-btn:hover {
  background-color: #ffa726;
}

/* pagination */
.pagination {
  display: flex;
  justify-content: center;
  gap: 10px;
  margin-top: 40px;
}

.pagination button {
  padding: 10px 15px;
  border: none;
  background-color: #ffe198;
  color: #fff;
  cursor: pointer;
  border-radius: 5px;
  transition: background-color 0.3s;
}

.pagination button:hover {
  background-color: #ffa726;
}

.pagination button.active {
  background-color: #ff9800;
}

.pagination button:disabled {
  background-color: #ddd;
  cursor: not-allowed;
}
</style>