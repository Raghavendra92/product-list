<template>
<div class="desktop-view">
  <div class="header-container">
    <img :src="Logo" alt="Product Image" />

    <div class="icon-bar">
      <div class="search-container">
        <div class="search-input-wrapper">
          <img :src="SearchIcon" alt="Search Icon" class="search-icon" />
          <input v-model="searchQuery" placeholder="Search" />
        </div>
        <button class="search-button" @click="handleSearch">Search</button>
      </div>
      <div class="icon-wrapper notification">
        <img src="@/assets/Gear.svg" alt="Notification Icon" />
        <span class="notification-dot"></span>
      </div>
      <div class="icon-wrapper">
        <img src="@/assets/Notifications.svg" alt="Settings Icon" />
      </div>
      <div class="icon-wrapper">
        <img src="@/assets/User.svg" alt="User Icon" />
      </div>
    </div>
  </div>
  <div>
    <div class="products-count">
      <b>Products</b> {{ filteredProducts.length }} of
      {{ products.length }} results
    </div>
    <table>
      <thead>
        <tr>
          <th :style="{'min-width': '70px'}">ID</th>
          <th :style="{'min-width': '144px'}">Status</th>
          <th :style="{'min-width': '125px'}" @click="sort('quantity')">Quantity</th>
          <th :style="{'min-width': '670px'}" @click="sort('product')">Product name</th>
          <th :style="{'min-width': '170px'}" class="prices-th" @click="sort('total')"><span>Prices</span><img src="@/assets/down.svg" alt="Down arrow Icon" /></th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="product in filteredProducts"
          :key="product.id"
          @click="openModal(product)"
        >
          <td :style="{'min-width': '70px'}">{{ product.id }}</td>
          <td :style="{'min-width': '144px'}"><span :class="['status-cell',product.quantity > 0 ? 'available': 'no-stock']">Status</span></td>
          <td :style="{'min-width': '125px'}">{{ product.quantity }}</td>
          <td :style="{'min-width': '670px'}" class="product-name">{{ product.product }}</td>
          <td :style="{'min-width': '170px'}" class="price">{{ product.total }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</div>

<div class="mobile-view">
    <div class="mobile-product-page">
        <!-- Header with logo and menu -->
        <header class="page-header">
        <img src="@/assets/Logo.png" alt="Logo" class="logo" />
        <div class="menu-container">
                <button class="menu-button" @click="toggleMenu"><img src="@/assets/menu.svg"/> </button>
        <div v-if="this.menuOpen" class="mobile-nav">
            <div class="icon-wrapper notification">
                <img src="@/assets/Gear.svg" alt="Notification Icon" />
                <span class="notification-dot"></span>
            </div>
            <div class="icon-wrapper">
                <img src="@/assets/Notifications.svg" alt="Settings Icon" />
            </div>
            <div class="icon-wrapper">
                <img src="@/assets/User.svg" alt="User Icon" />
            </div>
        </div>
        </div>
        </header>

        <!-- Search Bar -->
        <div class="search-bar">
          <img :src="SearchIcon" alt="Search Icon" class="search-icon" />
          <input v-model="searchQuery" placeholder="Search" />
        <button class="search-button">Search</button>
        </div>

        <!-- Product List Heading -->
        <h3 class="products-title">
        Products <span class="results-count">{{ filteredProducts.length }} of
      {{ products.length }} results</span>
        </h3>

        <!-- Product List -->
        <div class="product-list">
        <div class="product-card header">Product name</div>
        <div v-for="product in filteredProducts" :key="product.id" @click="openModal(product)" class="product-card">
            <div class="product-name">{{ product.product }}</div>
            <div class="product-info">
            <span>{{ product.serial }}</span> - <span>Qty: {{ product.quantity }}</span>
            </div>
        </div>
        </div>
    </div>
</div>

<ProductModal
    v-if="selectedProduct"
    :product="selectedProduct"
    @close="closeModal"
/>
</template>

<script>
import ProductModal from "./ProductModal.vue";

export default {
  components: {
    ProductModal,
  },
  data() {
    return {
      products: [], // Mock data fetched in mounted()
      searchQuery: "",
      sortKey: "",
      sortOrder: 1, // 1 for ascending, -1 for descending
      selectedProduct: null,
      Logo: require("@/assets/Logo.png"),
      SearchIcon: require("@/assets/search.png"),
      menuOpen: false,
    };
  },
  computed: {
    filteredProducts() {
      const filtered = this.products?.filter((product) =>
        product.product.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
      if (this.sortKey) {
        return filtered.sort((a, b) => {
          if (a[this.sortKey] < b[this.sortKey]) return -this.sortOrder;
          if (a[this.sortKey] > b[this.sortKey]) return this.sortOrder;
          return 0;
        });
      }
      return filtered;
    },
  },
  methods: {
    sort(key) {
      this.sortKey = key;
      this.sortOrder *= -1;
    },
    openModal(product) {
      this.selectedProduct = product;
    },
    closeModal() {
      this.selectedProduct = null;
    },
    toggleMenu(){
        this.menuOpen = !this.menuOpen;
    }
  },
  async mounted() {
    // Replace with API call in future
    this.products = await new Promise((resolve) => {
      setTimeout(() => {
        resolve([
          {
            product: "Macbook Pro 16 inch (2020 ) For Sale",
            serial: "BA9212320",
            id: 1374,
            quantity: 122,
            total: 854.08,
            image:
              "https://superapple.cz/wp-content/uploads/2019/11/Apple_16-inch-MacBook-Pro_111319-800x445.jpg",
          },
          {
            product: "Gaming Chair, local pickup only",
            serial: "XP8619376",
            id: 3933,
            quantity: 245,
            total: 943.65,
          },
          {
            product: "Macbook Air 13 inch(2020 ) For Sale",
            serial: "KH9212924",
            id: 9374,
            quantity: 134,
            total: 779.58,
            image:
              "https://images.iphonemod.net/wp-content/uploads/2020/03/apple-released-new-macbook-air-13-inch-2020-2-1024x828.png",
          },
          {
            product: "Heimer Miller Sofa (Mint Condition)",
            serial: "SD9212969",
            id: 5560,
            quantity: 26,
            total: 275.43,
            image: "https://www.pngall.com/wp-content/uploads/4/Sofa-PNG.png",
          },
          {
            product: "iPad Pro 2017 Model",
            serial: "012921097",
            id: 6065,
            quantity: 76,
            total: 475.22,
            image:
              "https://brain-images-ssl.cdn.dixons.com/6/3/10165836/l_10165836_002.jpg",
          },
          {
            product: "Gopro hero 7 (with receipt)",
            serial: "GM6812978",
            id: 4349,
            quantity: 47,
            total: 219.78,
            image:
              "https://gadgetsin.com/uploads/2018/10/gopro_hero7_black_waterproof_4k_action_camera_1.jpg",
          },
          {
            product: "Dell Computer Monitor",
            serial: "HQ0192837",
            id: 9359,
            quantity: 54,
            total: 105.55,
            image: "https://www.techpowerup.com/img/08-09-27/320-7339.jpg",
          },
          {
            product: "AirPods Pro",
            serial: "LK89471045",
            id: 8829,
            quantity: 132,
            total: 928.41,
            image:
              "https://scoprilamela.it/wp-content/uploads/2020/09/airpods-pro.jpg",
          },
          {
            product: "Playstation 4 Limited Edition",
            serial: "TU23182451",
            id: 5045,
            quantity: 15,
            total: 473.85,
          },
          {
            product: "DJI Mavic Pro 2",
            serial: "JD45712035",
            id: 3536,
            quantity: 39,
            total: 576.28,
            image:
              "https://images.wired.it/wp-content/uploads/2016/09/28193850/1475077129_Dji-Mavic-Pro-.jpg",
          },
        ]);
      }, 500);
    });
  },
};
</script>

<style scoped lang="scss">
.desktop-view {
.header-container {
  display: flex;
  justify-content: space-between;
  margin-bottom: 40px;
  margin-right: 20px;
}

.search-container {
  display: flex;
  align-items: center;
  gap: 10px;

  .search-input-wrapper {
    display: flex;
    align-items: center;
    border: 1px solid #ddd;
    border-radius: 5px;
    padding: 10px;
    position: relative;

    input {
      border: none;
      outline: none;
      padding-left: 30px;
      font-size: 16px;
      width: 200px;
    }

    .search-icon {
      position: absolute;
      left: 10px;
      color: #ccc;
    }
  }

  button {
    background-color: #605dec;
    color: white;
    border: none;
    border-radius: 5px;
    padding: 10px 20px;
    cursor: pointer;
    font-size: 16px;
  }
}

.icon-bar {
  display: flex;
  align-items: center;
  gap: 10px;
}

.products-count {
    margin-bottom: 15px;
}

.prices-th{
    display: flex;
    justify-content: space-around;
}
}

.mobile-view {
    .mobile-product-page {
 font-family: 'Nunito Sans', sans-serif;;
}

/* Header with logo and menu button */
.page-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-bottom: 10px;
}

.logo {
  max-width: 210px;
}

.menu-button {
  background: none;
  border: none;
  font-size: 24px;
  cursor: pointer;
}

/* Search bar */
.search-bar {
    display: flex;
    align-items: center;
    padding: 10px 0px;
    position: relative;
    gap: 20px;
}

.search-bar input {
  padding: 18px;
  border: 1px solid #ccc;
  border-radius: 4px;
  padding-left: 40px;
  font-size: 16px;  
}

.search-button {
  padding: 20px 22px;
  background-color: #605DEC;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

/* Product list heading */
.products-title {
  font-size: 18px;
  font-weight: bold;
  padding-bottom: 10px;
}

.results-count {
  font-size: 14px;
  color: gray;
}

/* Product card styles */
.product-list {
  display: flex;
  flex-direction: column;
  border: 1px solid #ddd;
  border-radius: 8px;
}

.product-card {
  border: 1px solid #ddd;
  padding: 15px;
  background-color: #fff;
}

.product-name {
  font-size: 16px;
}

.product-info {
  font-size: 14px;
  color: gray;
  padding-top: 5px;
}

.search-icon {
    position: absolute;
    left: 10px;
}

.product-card.header{
    text-align: center;
    font-size: 16px;
    font-weight: 700;
    line-height: 20px;
    padding: 20px;
}

.menu-container {
  position: relative;
}

.mobile-nav {
  position: absolute;
  top: 50px; /* Adjust as needed */
  left: 0;
  background-color: white;
  border: 1px solid #ddd;
  border-radius: 8px;
  box-shadow: 0px 4px 12px rgba(0, 0, 0, 0.1);
  width: 200px;
  padding: 10px;
  z-index: 10;
}

.icon-wrapper {
  display: flex;
  align-items: center;
  padding: 10px;
  cursor: pointer;
}

.icon-wrapper:hover {
  background-color: #f5f5f5;
  border-radius: 4px;
}
}

@media (max-width: 768px){
.desktop-view {
    display: none;
}
}

@media (min-width: 768px){
.mobile-view {
    display: none;
}
}
</style>
