<template>
    <header>
        <!-- Thanh tìm kiếm -->
        <div class="search-bar">
            <input type="text" placeholder="Tìm kiếm sản phẩm..." v-model="searchQuery" @input="performSearch" />
            <button @click="performSearch">Tìm kiếm</button>
        </div>

        <div class="container">
            <div class="logo">
                <img src="/Images/logo.png" alt="Logo Nhà Hàng" />
            </div>
            <nav>
                <ul>
                    <li><router-link to="/">Trang Chủ</router-link></li>
                    <li><router-link to="/thucdon">Thực Đơn</router-link></li>
                    <li><router-link to="/gioithieu">Giới Thiệu</router-link></li>
                    <li><router-link to="/lienhe">Liên Hệ</router-link></li>
                    <li><router-link to="/tintuc">Tin Tức</router-link></li>
                    <li><router-link to="/register">Đăng Ký</router-link></li>
                    <li><router-link to="/login">Đăng Nhập</router-link></li>
                </ul>
            </nav>
            <div v-if="user">
                <p>Xin chào, {{ user.username }}</p>
                <button @click="logout">Đăng xuất</button>
            </div>
            <div class="cta">
                <router-link to="/cart" class="cta-button">Giỏ Hàng</router-link>
                <p class="cart-count">{{ totalQuantity }}</p>
            </div>
        </div>
    </header>

    <!-- Hiển thị kết quả tìm kiếm -->
    <div v-if="searchResults.length > 0" class="search-results">
        <h2>Kết quả tìm kiếm</h2>
        <div class="product-list">
            <div v-for="product in searchResults" :key="product.id" class="product-item">
                <img :src="product.image" alt="Product Image" />
                <h3>{{ product.name }}</h3>
                <p>{{ product.description }}</p>
                <p>Price: {{ product.price }}</p>
                <button @click="addToCart(product)">Thêm vào Giỏ</button>
            </div>
        </div>
    </div>

    <!-- lấy nội dung component được link tới -->
    <router-view />
</template>

<script>
import eventBus from '@/eventBus'
import items from '@/data/items'   // Đường dẫn tới file items.js
import cart from '@/data/cart';

export default {
    data() {
        return {
            user: JSON.parse(localStorage.getItem('currentuser')) || null,
            searchQuery: '', // Biến lưu nội dung tìm kiếm
            products: [...items], // Các sản phẩm lấy từ items
            searchResults: [], // Kết quả tìm kiếm
            cart,
        }
    },
    computed: {
        totalQuantity() {
            return this.cart.reduce((total, item) => total + item.quantity, 0)
        }
    },
    created() {
        eventBus.on('loginSuccess', (user) => {
            this.user = user
        })
    },
    beforeUnmount() {
        eventBus.off('loginSuccess')
    },
    methods: {
        logout() {
            localStorage.removeItem('currentuser')
            this.cart.splice(0, this.cart.length);
            this.user = null
            this.$router.push('/')
        },
        performSearch() {
            // Nếu ô tìm kiếm trống, không hiển thị kết quả
            if (this.searchQuery.trim() === '') {
                this.searchResults = []; // Xóa kết quả tìm kiếm
            } else {
                // Lọc kết quả tìm kiếm theo tên sản phẩm
                this.searchResults = this.products.filter(product =>
                    product.name.toLowerCase().includes(this.searchQuery.toLowerCase())
                );
            }
        },
        addToCart(product) {
            // Hàm thêm sản phẩm vào giỏ hàng
            console.log("Product added to cart:", product);
        }
    }
}
</script>

<style>
/* Các style cho trang */
.search-bar {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 10px;
}

.search-bar input {
    width: 250px;
    padding: 8px;
    border: 1px solid #ddd;
    border-radius: 4px;
    margin-right: 10px;
}

.search-bar button {
    padding: 8px 15px;
    background-color: #fcb034;
    color: #fff;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.3s ease;
}

.search-bar button:hover {
    background-color: #ffa726;
}

.search-results {
    padding: 20px;
    text-align: center;
}

.product-list {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
    justify-content: center;
}

.product-item {
    border: 1px solid #ddd;
    padding: 15px;
    width: 200px;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    text-align: center;
}

.product-item img {
    width: 100%;
    height: auto;
    border-radius: 8px;
}

.product-item h3 {
    font-size: 18px;
    margin: 10px 0;
}

.product-item p {
    font-size: 14px;
    color: #555;
}

.product-item button {
    padding: 8px 12px;
    background-color: #fcb034;
    color: #fff;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.3s ease;
}

.product-item button:hover {
    background-color: #ffa726;
}

.container {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 20px;
    background-color: #fff;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.logo img {
    height: 50px;
    transition: transform 0.3s ease;
}

.logo img:hover {
    transform: scale(1.1);
}

nav ul {
    list-style: none;
    display: flex;
    margin: 0;
    padding: 0;
}

nav ul li {
    margin: 0 15px;
}

nav ul li a {
    text-decoration: none;
    color: #000;
    font-weight: bold;
    transition: color 0.3s ease;
}

nav ul li a:hover {
    color: #fcb034;
}

.cta {
    display: flex;
    align-items: center;
    position: relative;
}

.cart-count {
    background-color: rgba(0, 0, 0, 0.9);
    color: #fff;
    font-size: 14px;
    padding: 5px 10px;
    border-radius: 50%;
    margin-left: 10px;
    position: absolute;
    top: -30px;
    right: 0;
}

.cta-button {
    padding: 10px 20px;
    background-color: #fcb034;
    color: #fff;
    text-decoration: none;
    border-radius: 25px;
    transition: background-color 0.3s ease, transform 0.3s ease;
}

.cta-button:hover {
    background-color: #ffa726;
    transform: scale(1.1);
}
</style>
