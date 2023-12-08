<template>
    <form @submit.prevent="handleSubmit">
        <div v-for="(value, key) in formData" :key="key">
            <label>{{ key }}</label>
            <template v-if="isObject(value)">
                <!-- Recursively render nested objects -->
                <nested-form :formData="value" />
            </template>
            <template v-else-if="Array.isArray(value)">
                <!-- Render nested arrays -->
                <div v-for="(item, index) in value" :key="index">
                    <nested-form :formData="item" />
                </div>
            </template>
            <template v-else>
                <!-- Render simple input for other types -->
                <input v-model="formFields[key]" />
            </template>
        </div>
        <button type="submit">Submit</button>
    </form>
</template>

<script>
export default {
    props: {
        formData: Object,
    },
    methods: {
        isObject(value) {
            return typeof value === "object" && value !== null && !Array.isArray(value);
        },
        handleSubmit() {
            // Handle form submission here
            console.log("Form submitted with data:", {
                prop: this.formData,
                mod: this.formFields,
            });
        },
    },
    computed: {
        formFields() {
            return this.formData;
        },
    },
};
</script>
