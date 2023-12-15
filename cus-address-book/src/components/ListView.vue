<!-- ListView.vue -->
<template>
    <div class="list-view">
        <div class="list-header">
      <div class="header-left">
        <h3>All Customers</h3>
        <p class="status">Active Members</p>
      </div>
      <div class="header-middle">
        <input type="text" placeholder="Search" />
      </div>
    </div>
    <div class="list-table">
      <div class="table-header">
        <div>Customer Name</div>
        <div>Company</div>
        <div>Phone Number</div>
        <div>Email</div>
        <div>Country</div>
        <div>Status</div>
      </div>
      <div class="table-row" v-for="customer in customers" :key="customer.id">
        <div>{{ customer.name }}</div>
        <div>{{ customer.company }}</div>
        <div>{{ customer.phone }}</div>
        <div>{{ customer.email }}</div>
        <div>{{ customer.country }}</div>
        <button @click="toggleStatus(customer)" :class="{ 'active': customer.status === 'Active', 'inactive': customer.status === 'Inactive' }">
          {{ customer.status }}
        </button>
      </div>
    </div>
    <!-- <Pagination
      :currentPage="currentPage"
      :totalPages="totalPages"
      :totalEntries="totalEntries" 
      :itemsPerPage="itemsPerPage"
      @page-change="changePage"
    /> -->
    <Pagination :totalPages="totalPages" :currentPage="currentPage" @pageChange="changePage" />
    </div>
  </template>
  
  <script>
  import Pagination from "@/components/Pagination.vue";

  export default {
    components: {
    Pagination,
  },
  data() {
    return {
      customers: [
        { id: 1, name: "Jane Cooper", company: "Microsoft", phone: "(225) 555-0118", email: "jane@microsoft.com", country: "United States", status: "Active" },
        { id: 2, name: "Floyd Miles", company: "Yahoo", phone: "(205) 555-0100", email: "floyd@yahoo.com", country: "Kiribati", status: "Inactive" },
        { id: 3, name: "Ronald  Richards", company: "Adobe", phone: "(302) 555- 0107", email: " ronald@adobe.com", country: "Kiribati", status: "Inactive" },
        { id: 4, name: "Marvin Mckinney", company: "Tesla", phone: "(252)555-0126", email: " marvin@tesla.com", country: "Kiribati", status: "Inactive" },
        { id: 5, name: "Jerome Bell ", company: "Google", phone: "(629) 555-0126", email: " jerome@google.com", country: "Kiribati", status: "Inactive" },
        { id: 6, name: "Kathryn Murphy", company: "Microsoft", phone: " (406) 555-0120", email: " kathryn@microsoft.com", country: "Kiribati", status: "Inactive" },
        { id: 7, name: "Jacod Jones", company: "Yahoo", phone: "(208)555-0112", email: " jacob@yahoo.com", country: "Kiribati", status: "Inactive" },
        { id: 8, name: "Kristin Watson", company: "Facebook", phone: "(205) 555-0100", email: "   kristin@facebook.com", country: "Kiribati", status: "Inactive" },
        { id: 9, name: "Floyd Miles", company: "Yahoo", phone: "(704) 555-0127", email: "floyd@yahoo.com", country: "Kiribati", status: "Inactive" },
        
      ],
      itemsPerPage: 8,
      currentPage: 1,
      searchQuery: "", // for search property
      totalEntries: 0,
    };
  },
  computed: {
    totalPages() {
      return Math.ceil(this.totalEntries / this.itemsPerPage);
    },

    paginatedCustomers() {
      const startIndex = (this.currentPage - 1) * this.itemsPerPage;
      const endIndex = startIndex + this.itemsPerPage;
      return this.customers.slice(startIndex, endIndex);
    },
  },
  methods: {
    
    updateTotalEntries(filteredCustomers) {
    this.totalEntries = filteredCustomers.length;
    console.log('Total Entries Updated:', this.totalEntries);
  },
    toggleStatus(customer) {
      customer.status = customer.status === "Active" ? "Inactive" : "Active";
    },
  
    changePage(page) {
      this.currentPage = page;
    },
  },
};
  </script>
  
  <style scoped>
  .list-view {
  background-color: white;
  padding: 20px;
  justify-content: center;
  align-items: center;
  margin: 150px;
  padding: 50px;
  border-radius: 10px;
  /* justify-content: center; */
}

.list-header {
  display: flex;
  justify-content: space-between;
  margin-bottom: 10px;
}

.header-left {
  display: flex;
  flex-direction: column;
}

.header-left h3 {
  color: black;
}

.status {
  color: green;
  font-size: 12px;
  border-width: 2px;
}

.header-middle input {
  padding: 5px;
  border-radius: 5px;
  border: 1px solid #ccc;
  align-items: center;
}

.list-table {
  background-color: white;
  border-radius: 10px;
  overflow: hidden;
  align-items: center;
}

.table-header {
  display: grid;
  grid-template-columns: repeat(6, 1fr);
  background-color: white;
  color: gray;
  padding: 10px;
}

.table-row {
  display: grid;
  grid-template-columns: repeat(6, 1fr);
  padding: 10px;
  border-bottom: 1px solid #ccc;
}

button {
  cursor: pointer;
  border: none;
  border-radius: 5px;
  padding: 5px;
  color: white;
  font-weight: bold;
  outline: none;
}

.active {
  background-color: lightgreen;
  color: darkgreen;
}

.inactive {
  background-color: lightcoral;
  color: darkred;
  border-color: darkred;
}
  </style>
  