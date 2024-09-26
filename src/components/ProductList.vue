<template>
    <div class="product-list">
      <h1>Список тачек</h1>
      <div class="products-container">
        <div v-for="product in products" :key="product.id" class="product mb-3">
          <img :src="product.imageUrl" alt="Изображение товара" class="product-image" />
          <h2>{{ product.name }}</h2>
          <p>Цена: {{ product.price }} ₽</p>
          <button @click="addToCart(product)" class="btn btn-heart">
            <span class="heart-icon">❤️</span> <!-- Символ сердца -->
          </button>
        </div>
      </div>
  
      <h2>Корзина</h2>
      <div v-if="cart.length > 0">
        <h3>Добавленные товары:</h3>
        <ul class="list-group">
          <li v-for="item in cart" :key="item.id" class="list-group-item">{{ item.name }} - {{ item.price }} ₽</li>
        </ul>
        <button @click="checkout" class="btn btn-primary mt-3">Оформить заказ</button>
      </div>
      <div v-else>
        <p>Корзина пуста.</p>
      </div>
  
      <OrderForm v-if="showOrderForm" />
    </div>
  </template>
  
  <script>
  import OrderForm from './OrderForm.vue';
  
  export default {
    components: {
      OrderForm
    },
    data() {
      return {
        products: [
          { id: 1, name: 'Молния', price: 100260, imageUrl: require('@/assets/mcvin.jpeg') },
          { id: 2, name: 'Маквин', price: 2898700, imageUrl: require('@/assets/metr.jpeg') },
          { id: 3, name: 'Делает кчау', price: 3010, imageUrl: require('@/assets/franc.jpeg') }
        ],
        cart: [],
        showOrderForm: false
      };
    },
    methods: {
      addToCart(product) {
        this.cart.push(product);
        console.log('Товар добавлен в корзину:', product);
      },
      checkout() {
        this.showOrderForm = true; // Показываем форму заказа
      }
    }
  }
  </script>
  
  <style scoped>
  .products-container {
    display: flex; /* Используем Flexbox для расположения товаров в строку */
    justify-content: center; /* Центруем по горизонтали */
    flex-wrap: wrap; /* Позволяем элементам переноситься на новую строку */
  }
  
  .product {
    border: 1px solid #000000; /* Рамка вокруг каждого товара */
    border-radius: 5px; /* Скругление углов */
    padding: 15px; /* Отступы внутри товара */
    margin: 10px; /* Отступы между товарами */
    background-color: white; /* Цвет фона товара */
    transition: box-shadow 0.3s; /* Эффект тени при наведении */
    width: 180px; /* Задаем ширину для товаров */
  }
  
  .product-image {
    max-width: 100%; /* Адаптивная ширина */
    height: auto; /* Сохраняем пропорции */
    margin-bottom: 10px; /* Отступ снизу */
  }
  
  .product:hover {
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1); /* Тень при наведении */
  }
  
  /* Стили для кнопки-сердца */
  .btn-heart {
    background: none; /* Убираем фоновый цвет */
    border: rgb(0, 0, 0); /* Убираем рамку */
    color: rgb(255, 255, 255); /* Цвет сердца */
    font-size: 24px; /* Размер сердца */
    cursor: pointer; /* Курсор при наведении */
    transition: transform 0.2s; /* Эффект трансформации при наведении */
  }
  
  .btn-heart:hover {
    transform: scale(1.2); /* Увеличиваем сердце при наведении */
  }
  </style>
  