<template>
    <div class="home-page">
        <Banner />
        <h1>TẤT CẢ SẢN PHẨM</h1>
        <div class="menu-items">
            <Product v-for="item in paginatedItems" :key="item.id" :product="item" />
        </div>
    </div>
    <!-- Phân trang -->
    <div class="pagination">
        <button @click="prevPage" :disabled="currentPage === 1">Trước</button>
        <button v-for="page in totalPages" :key="page" @click="goToPage(page)"
            :class="{ active: currentPage === page }">
            {{ page }}
        </button>
        <button @click="nextPage" :disabled="currentPage === totalPages">Tiếp</button>
    </div>
</template>


<script>
import Banner from './ComBanner.vue';
import Product from './ComProduct.vue';
import items from '../data/items';

export default {
    name: 'ComHome',
    components: { Banner, Product },
    data() {
        return {
            menuItems: items,
            currentPage: 1,
            itemsPerPage: 3
        }
    },
    computed: {
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

}
</script>

<style scoped>
.home-page {
    text-align: center;
}

.search-bar {
    margin: 20px;
}

.search-bar input {
    padding: 10px;
    width: 80%;
    font-size: 16px;
}

.menu-items {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
    justify-content: center;
    margin-bottom: 40px;
}

/* pagination */
.pagination {
    display: flex;
    justify-content: center;
    gap: 10px;
    margin-top: 40px;
    margin-bottom: 30px;
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
