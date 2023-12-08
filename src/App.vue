<template>
    <div>
        <nested-form :formData="nestedJsonData" />
    </div>
</template>

<script>
import NestedForm from "@/components/NestedForm.vue"; // Adjust the path based on your project structure

export default {
    components: {
        NestedForm,
    },
    data() {
        return {
            nestedJsonData: {
                // Your nested JSON data goes here
                // Example:
                name: "John Doe",
                address: {
                    street: "123 Main St",
                    city: "Example City",
                },
                hobbies: ["Reading", "Coding"],
            },
        };
    },
};
</script>
