<template>
    <div v-if="this.cart.length == 0">
        <img src="@/assets/cart-empty.png" class="cart-image">
    </div>
    <div v-else class="modal-content">
        <table class="table text-center cart-table">
            <tr>
                <th>HÌNH</th>
                <th>SẢN PHẨM</th>
                <th>Đơn giá</th>
                <th>Số lượng</th>
                <th>Tiền</th>
                <th>Hành động</th>
            </tr>
            <tr v-for="item in cart" :key="item.id">
                <td><img :src="item.image" class="product-image"></td>
                <td>{{ item.name }}</td>
                <td>{{ item.price }}</td>
                <td>
                    <button class="decrease-btn" @click="decreaseQuantity(item)">−</button>
                    {{ item.quantity }}
                    <button class="increase-btn" @click="increaseQuantity(item)">+</button>
                </td>
                <td>{{ item.price * item.quantity }}</td>
                <td><button class="btn btn-danger" @click="deleteProduct(item)">Xóa</button></td>
            </tr>
            <tr>
                <th></th>
                <th></th>
                <th>Tổng tiền</th>
                <th>{{ tongSoLuong }}</th>
                <th>{{ tongTien }}</th>
                <th><button class="btn btn-danger" @click="xoaHet()">Xóa tất cả sản phẩm</button></th>
            </tr>
        </table>

        <!-- Form thông tin khách hàng và thanh toán -->
        <div class="checkout-container">
            <div class="customer-info">
                <h3>Thông tin người đặt</h3>
                <div class="group">
                    <label>Tên:</label>
                    <input v-model="customerName" type="text" placeholder="Nhập tên của bạn" required />
                </div>
                <div class="group">
                    <label>Số điện thoại:</label>
                    <input v-model="customerPhone" type="tel" placeholder="Nhập số điện thoại của bạn" required />
                </div>
                <div class="group">
                    <label>Địa chỉ giao hàng:</label>
                    <textarea v-model="customerAddress" placeholder="Nhập địa chỉ giao hàng" rows="3"
                        required></textarea>
                </div>
            </div>

            <div class="payment-info">
                <h3>Thông tin thanh toán</h3>
                <label>Phương thức thanh toán:</label>
                <select v-model="paymentMethod">
                    <option value="cash">Thanh toán khi nhận hàng</option>
                </select>
                <button class="btn btn-success order-btn" @click="placeOrder">Đặt hàng</button>
            </div>
        </div>
    </div>
    <!-- Dialog thông báo đặt hàng thành công -->
    <transition name="fade">
        <div v-if="showDialog" class="dialog-overlay">
            <div class="dialog-box">
                <h3>Đặt hàng thành công!</h3>
                <p>Cảm ơn bạn đã đặt hàng!</p>
                <button class="btn btn-primary" @click="closeDialog">OK</button>
            </div>
        </div>
    </transition>
</template>


<script>
import cart from '@/data/cart'
import items from '@/data/items'

export default {
    data() {
        return {
            cart: cart,
            customerName: '',
            customerPhone: '',
            customerAddress: '',
            paymentMethod: 'cash',
            showDialog: false
        }
    },
    computed: {
        tongTien() {
            return this.cart.reduce((total, item) => total + item.price * item.quantity, 0)
        },
        tongSoLuong() {
            return this.cart.reduce((total, item) => total + item.quantity, 0)
        },
        totalQuantity() {
            return this.cart.reduce((total, item) => total - item.quantity, 0)
        }
    },
    methods: {
        deleteProduct(item) {
            const cartItemIndex = this.cart.findIndex(x => x.id === item.id);

            if (cartItemIndex !== -1) {
                const cartItem = this.cart[cartItemIndex];
                const productInStock = items.find(x => x.id === item.id);
                if (productInStock) {
                    productInStock.stock += cartItem.quantity;
                }
                this.cart.splice(cartItemIndex, 1);
            }
        },
        xoaHet() {
            this.cart.forEach(item => {
                const productInStock = items.find(x => x.id === item.id);
                if (productInStock) {
                    productInStock.stock += item.quantity;
                }
            })
            this.cart.splice(0, this.cart.length);
        },
        increaseQuantity(item) {
            const productold = items.find(x => x.id === item.id)
            if (productold && productold.stock > 0) {
                item.quantity++
                productold.stock--
            } else {
                alert("Không đủ hàng trong kho!");
            }
        },
        decreaseQuantity(item) {
            if (item.quantity > 1) {
                const productold = items.find(x => x.id === item.id)
                item.quantity--
                productold.stock++
            } else {
                this.deleteProduct(item)
            }
        },
        placeOrder() {
            if (this.customerName && this.customerPhone && this.customerAddress) {
                this.showDialog = true;
                this.xoaHet();
            } else {
                alert("Vui lòng điền đầy đủ thông tin người đặt.");
            }
        },
        closeDialog() {
            this.showDialog = false;
        }
    }
}

</script>

<style>
.btn-danger {
    background-color: red;
    color: white;
    border: none;
    padding: 5px 10px;
    border-radius: 5px;
    cursor: pointer;
}

.cart-image {
    width: 400px;
    height: 400px;
    object-fit: cover;
    margin: 10px auto;
}

/* dialog */
.fade-enter-active,
.fade-leave-active {
    transition: opacity 0.5s;
}

.fade-enter,
.fade-leave-to {
    opacity: 0;
}

.dialog-overlay {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 1000;
}

.dialog-box {
    background-color: #fff;
    padding: 20px;
    border-radius: 10px;
    text-align: center;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    width: 250px;
    height: 150px;
}

.dialog-box h3 {
    color: #e65100;
}

.dialog-box button {
    background-color: #ffa726;
    border: none;
    padding: 10px 20px;
    cursor: pointer;
    color: white;
    border-radius: 5px;
    margin-top: 10px;
}

.dialog-box button:hover {
    background-color: #ff9800;
}

.modal-content {
    margin: 20px auto;
    padding: 20px;
    background-color: #fff;
    border-radius: 10px;
    max-width: 1200px;
    /* box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1); */
}

.cart-table {
    width: 100%;
    margin-bottom: 20px;
}

.product-image {
    height: 100px;
    width: 100px;
}

.increase-btn,
.decrease-btn {
    padding: 5px;
    font-size: 14px;
    background-color: #ffa726;
    border: none;
    cursor: pointer;
    transition: background-color 0.3s;
    color: #fff;
    margin: 0 5px;
}

.increase-btn:hover,
.decrease-btn:hover {
    background-color: #ff9800;
}

.checkout-container {
    display: flex;
    justify-content: space-between;
    gap: 20px;
    margin-top: 20px;
}

.customer-info,
.payment-info {
    display: flex;
    flex-direction: column;
    align-items: start;
    justify-content: start;
    background-color: #fff3e0;
    padding: 20px;
    border-radius: 10px;
    width: 45%;
}

.customer-info h3,
.payment-info h3 {
    color: #e65100;
    margin-bottom: 15px;
}

.group {
    display: flex;
    flex-direction: column;
    align-items: start;
    justify-content: start;
    width: 96%;
}

.group label {
    margin-top: 10px;
}

input,
textarea,
select {
    width: 100%;
    padding: 10px;
    margin-top: 10px;
    margin-right: 10px;
    border-radius: 5px;
    border: 1px solid #ddd;
    outline: none;
    font-size: 14px;
}

.order-btn {
    margin-top: 20px;
    background-color: #ffa726;
    border: none;
    padding: 10px 16px;
    color: white;
    cursor: pointer;
    transition: background-color 0.3s;
    border-radius: 5px;
    font-size: 14px;
}

.order-btn:hover {
    background-color: #ff9800;
}
</style>
