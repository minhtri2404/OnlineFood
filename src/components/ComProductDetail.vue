<template>
    <div class="menu-item">
        <img :src="product.image" :alt="product.name" class="menu-image" />
        <div class="menu-info">
            <h3>{{ product.name }}</h3>
            <p>{{ product.description }}</p>
            <p class="price">{{ product.price }} VND</p>
        </div>
        <div v-if="product.stock == 0">
            <p>Hết Hàng</p>
        </div>
        <div v-else>
            <button @click="addToCart(product)" class="add-to-cart-btn">Thêm vào giỏ hàng</button>
        </div>
    </div>

</template>

<script>
import items from '@/data/items'
import cart from "@/data/cart"
import users from '@/data/users'
export default {
    data() {
        return {
            product: {},
            cart: cart,
            loggedInUser: null,
            users: users,
        }
    },
    mounted() {
        // Lấy id từ URL (productDetail route)
        let id = this.$route.params.id;
        this.product = items.find(item => item.id == id);
        this.loggedInUser = JSON.parse(localStorage.getItem('currentuser')) || null;

    },
    computed: {
        isUserLoggedIn() {
            return this.loggedInUser !== null;
        }
    },
    methods: {
        addToCart(product) {
            if (!this.isUserLoggedIn) {
                alert('Bạn cần đăng nhập để thêm sản phẩm vào giỏ hàng.');
                return;
            }
            const existingProduct = this.cart.find(item => item.id == product.id);
            if (existingProduct) {
                if (product.stock > 0) {
                    existingProduct.quantity += 1;
                    product.stock--;
                }
            } else {
                if (product.stock > 0) {
                    const newProduct = { ...product, quantity: 1 };
                    this.cart.push(newProduct);
                    product.stock--;
                }
            }

            // Cập nhật giỏ hàng vào localStorage để duy trì khi reload trang
            localStorage.setItem('cart', JSON.stringify(this.cart));
        },
        login(userId) {
            this.loggedInUser = this.users.find(user => user.id === userId);
            localStorage.setItem('currentuser', JSON.stringify(this.loggedInUser));
        },
    }

}
</script>

<style>
.menu-item {
    width: 300px;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
    border-radius: 10px;
    overflow: hidden;
    background-color: #fff;
    transition: transform 0.3s;
    margin: 20px auto;
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
    margin-bottom: 20px;
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
</style>