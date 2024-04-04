<template>
    <div class="page">
      <h4>Thêm Liên hệ</h4>
      <ContactForm @submit:contact="addContact"/>
      <p>{{ message }}</p>
    </div>
  </template>
  
  <script>
  import ContactForm from "@/components/ContactForm.vue";
  import ContactService from "@/services/contact.service";
  
  export default {
    components: {
      ContactForm,
    },
    data() {
      return {
        message: "",
      };
    },
    methods: {
      async addContact(newContactData) {
        try {
          
          const result = await ContactService.create(newContactData);
          if(result){
            this.message = "Liên hệ được thêm thành công.";
          }
          else{
            this.message = "Liên hệ đã tồn tại.";
          }
        } catch (error) {
          this.message = "An error occurred while adding the contact.";
        }
      },
    },
  };
  </script>
  