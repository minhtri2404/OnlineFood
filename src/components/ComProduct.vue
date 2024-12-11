<template>
    <div class="menu-item">
        <router-link :to="{ name: 'ProductDetail', params: { id } }" class="menu-link">
            <img :src="product.image" :alt="product.name" class="menu-image" />
            <div class="menu-info">
                <h3>{{ product.name }}</h3>
                <p>{{ product.description }}</p>
                <p class="price">{{ product.price }} VND</p>
            </div>
        </router-link>
    </div>
</template>

<script>
export default {
    // nhận giá trị từ cha props:['bientruyen']
    props: ['product'],
    data() {
        return {
            //lấy id của sản paamr truyền qua
            
            id: this.product.id
        }
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
    margin-top: 20px;
}

.menu-link {
    text-decoration: none;
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
</style>