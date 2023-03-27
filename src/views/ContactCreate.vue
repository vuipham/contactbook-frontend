<template>
    <div v-if="contact" class="page">
        <h4>Tao Liên hệ</h4>
        <ContactForm
            :contact="contact"
            @submit:contact="addContact"
            
        />
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
            contact: ContactForm,
            message: "",
        };
    },
    methods: {
        async addContact(data) {
            console.log(data)
            try {
                await ContactService.create(data);
                this.message = "Liên hệ được tao thành công.";
            } catch (error) {
                console.log(error);
            }
        },
    },
    created() {
        this.addContact(this.data);
        this.message = "";
    },
};
</script>