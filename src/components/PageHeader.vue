<!-- <template>
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
      <div class="icon-wrapper">
        <img src="@/assets/Notifications.png" alt="Settings Icon" />
      </div>
      <div class="icon-wrapper notification">
        <img src="@/assets/Gear.svg" alt="Notification Icon" />
        <span class="notification-dot"></span>
      </div>
      <div class="icon-wrapper">
        <img src="@/assets/User.png" alt="User Icon" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      Logo: require("@/assets/Logo.png"),
      SearchIcon: require("@/assets/search.png"),
    };
  },
};
</script>

<style scoped lang="scss">
.header-container {
  display: flex;
  justify-content: space-between;
  margin-bottom: 40px;
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
</style> -->
