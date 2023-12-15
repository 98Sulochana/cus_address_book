<!-- eslint-disable vue/multi-word-component-names -->
<!-- AddCustomerForm.vue -->
<template>
  <div class="scroll-container">
  <div class="add-customer-form">
    <h2>Add New Customer</h2>
    <form @submit.prevent="submitForm">
      <!-- Customer Details -->
      <div class="form-section">
        <input type="text" placeholder="Customer Name" v-model="newCustomer.name" required />
        <div class="underline"></div>
        <input type="text" placeholder="Company" v-model="newCustomer.company" required />
        <input type="text" placeholder="Contact Phone" v-model="newCustomer.phone" required pattern="\d{10}" />
        <input type="email" placeholder="E-mail" v-model="newCustomer.email" required />
        <input type="text" placeholder="Country" v-model="newCustomer.country" required />

        <h4>Address Details</h4>
        <div v-for="(address, index) in newCustomer.addresses" :key="index" class="address-section">
          <div class="horizontal-inputs">
            <input type="text" v-model="address.number" placeholder="Number" required />
            <div class="underline"></div>
            <input type="text" v-model="address.street" placeholder="Street" required />
          </div>
          <input type="text" v-model="address.cityState" placeholder="City, State" required />
          <div class="underline"></div>
          <button type="button" @click="removeAddress(index)" class="delete-button">DELETE</button>
        </div>
        <button type="button" @click="addAddress" class="add-button">ADD</button>
        <button type="submit" class="submit-button">Submit</button>
        </div>
      
    </form>
  </div>
</div>
</template>
  
<script>
  export default {
  data() {
    return {
      newCustomer: {
        name: "",
        company: "",
        phone: "",
        email: "",
        country: "",
        addresses: [{ number: "", street: "", cityState: "" }],
      },
    };
  },
  methods: {
    addAddress() {
      this.newCustomer.addresses.push({ number: "", street: "", cityState: "" });
    },
    removeAddress(index) {
      this.newCustomer.addresses.splice(index, 1);
    },
    submitForm() {
      console.log("Form submitted:", this.newCustomer);
    },
  },
};
</script>

 <style>
 .scroll-container {
  max-height: 700px; 
  overflow-y: auto; 
  align-items: center;
  justify-content: center;
}
 .add-customer-form {
   background-color: #f0f0f0;
   padding: 20px;
   border-radius: 10px;
   margin: 20px auto;
   width: 350px;
   height: auto;
   display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin-left: 10%;
  margin-right: 10%;
  font-family: sans-serif;
  overflow-y: auto;
 }
 .horizontal-inputs {
  display: flex;
  gap: 10px;
}
 form {
   display: grid;
   grid-template-columns: repeat(2, 1fr);
   gap: 10px;
 }
 
 .form-section {
   margin-bottom: 20px; 
   position: relative;
   margin-left: 10px;
   line-height: 50px;
 }
 
 .form-section input,
 .address-section input {
   border: none;
   padding: 5px;
   width: calc(100% - 10px);
   border-bottom: 1px solid #000; 
 }
 
 .address-section {
   display: grid;
   grid-template-columns: repeat(1, 1fr);
   gap: 5px;
   margin-bottom: 20px; 
 }
 
 .delete-button {
   background-color: white;
   color: red;
   border-color: red;
   border-radius: 10px;
   padding: 5px;
   cursor: pointer;
   width: 70px;
 }
 
 .add-button {
   background-color: white;
   color: green;
   border-color: green;
   border-radius: 10px;
   width: 100px;
   padding: 5px;
   cursor: pointer;
 }
 
 .submit-button {
   grid-column: span 2;
   background-color: green;
   color: white;
   border: none;
   border-radius: 5px;
   padding: 7px;
   width: 200px;
   cursor: pointer;
 }
 .underline {
   position: absolute;
   bottom: 0;
   left: 0;
   right: 0;
   height: 1px;
   background-color: #000;
 }
 .validation-error {
  color: red;
  margin-top: 5px;
}
 </style>