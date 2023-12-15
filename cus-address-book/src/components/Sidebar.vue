<!-- eslint-disable vue/multi-word-component-names -->
<!-- Sidebar.vue -->
<template>
    <div class="sidebar">
    <div class="sidebar-header">
      <img :src="require('@/assets/dashboard.png')" alt="Dashboard Icon" class="icon"><h2><b>Dashboard</b></h2>
    </div>
    <ul>
      <li v-for="item in menuItems" :key="item.id" @click="handleItemClick(item)" :class="{ 'active': activeItem === item.name }">
        <img :src="require(`@/assets/${item.icon}.png`)" alt="Menu Icon" class="menu-icon">
        <i :class="item.icon"></i> {{ item.name }}
      </li>
    </ul>
    </div>
  </template>
  
  <script>
  export default {
  data() {
    return {
      menuItems: [
        { id: 1, name: "Dashboard", icon: "dashboard-icon" },
        { id: 2, name: "Product", icon: "product-icon" },
        { id: 3, name: "Customers", icon: "customer-icon" },
        { id: 4, name: "Income", icon: "income-icon" },
        { id: 5, name: "Promote", icon: "promote-icon" },
        { id: 6, name: "Help", icon: "help-icon" },
      ],
    };
  },
  methods: {
    handleItemClick(item) {
      this.$emit("menu-click", item);
    },
  },
};
  </script>
  
  <style>
 .sidebar {
  width: 250px;
  background-color: white;
}
.icon {
  width:25px;
  height: 25px;
}
.menu-icon{
  width:20px;
  height: 20px;
}

.sidebar-header {
  display: flex;
  background-color: white;
  color: black;
  padding: 10px;
  text-align: center;
  font-family: sans-serif;
  align-items: center;
}

.sidebar ul li.active {
  background-color: purple;
  color: white;
}
ul {
  list-style-type: none;
  padding: 0;
}

li {
  padding: 10px;
  cursor: pointer;
  font-family: sans-serif;
  font-size: medium;
  align-items: center;
}
/* 
li:hover {
  background-color: lightgray;
} */
</style>
  