<!-- eslint-disable vue/multi-word-component-names -->
<template>
    <div class="popup">
      <AddCustomerForm @submit="submitForm" @close="closePopup" />
    </div>
  </template>
  
  <script>
  import AddCustomerForm from "@/components/AddCustomerForm.vue";
  
  export default {
    components: {
      AddCustomerForm,
    },
    methods: {
      submitForm(formData) {
        console.log("Form submitted:", formData);
        this.closePopup();
      },
      closePopup() {
        this.$emit("close");
      },
    },
  };
  </script>
  
  <style scoped>
  .popup {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    /* background: white; */
    padding: 20px;
    border-radius: 10px;
    z-index: 1000;
    margin-top: 50px;
    margin-bottom: 80px;
  }
  </style>
  