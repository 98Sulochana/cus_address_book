 <template>
    <div id="app">
      <Sidebar @menu-click="handleMenuClick" :activeItem="activeMenuItem" />
      <div class="content">
        <div class="overlay" v-show="showAddForm" @click="hideAddCustomerForm"></div>
        <div class="header">
          <div class="greeting">
            <p>Hello Evano <span class="wave-icon">👋,</span></p>
          </div>
        </div>
       
       <!-- <div class="hello-text-line">
         <div class="line"></div>
         <div class="hello-text">
           Hello, {{ username }}
       </div>
      </div> -->
        <div class="floating-button" @click="toggleAddCustomerForm">+</div>
        <AddCustomerFormPopup v-show="showAddForm" @close="hideAddCustomerForm" />
        <ListView v-show="activeMenuItem === 'Customers'" />
      </div>
    </div>
  </template>

<script>
import Sidebar from "@/components/Sidebar.vue";
import ListView from "@/components/ListView.vue";
import AddCustomerFormPopup from "@/components/AddCustomerFormPopup.vue";

export default {
  components: {
    Sidebar,
    // AddCustomerForm,
    ListView,
    AddCustomerFormPopup,
  },
  data() {
    return {
      // username: "John Doe",
      showAddForm: false,
      activeMenuItem: "",
    };
  },
  methods: {
    toggleAddCustomerForm() {
      this.showAddForm = !this.showAddForm;
    },
    hideAddCustomerForm() {
      this.showAddForm = false;
    },
    handleMenuClick(item) {
      this.activeMenuItem = item.name;
      console.log(`Clicked on ${item.name}`);
    },
     },
};
</script>

<style>
#app {
  display: flex;
  background-color: #e1e1ea;
  flex-direction: row;
}
/* .sidebar {
  width: 250px;
  background-color: white;
} */
.overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  display: none;
  z-index: 999;
}

.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: e1e1ea;
  padding: 10px;
}

.greeting {
  display: flex;
  align-items: center;
}

.greeting p {
  margin: 0;
  margin-left: 10px;
}

.wave-icon {
  font-size: 20px;
}

.floating-button {
  position: fixed;
  top: 20px;
  right: 20px;
  width: 40px;
  height: 40px;
  background-color: lightgreen;
  color: darkgreen;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 20px;
  cursor: pointer;
  box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.1);
}

</style>


