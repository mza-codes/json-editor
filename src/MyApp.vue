<template>
    <div id="app">
        <form @submit.prevent="handleSubmit">
            <template v-for="(value, key) in formData" :key="key">
                <template v-if="isObject(value)">
                    <label :for="key">{{ key }}:</label>
                    <div :key="key">
                        <ObjectForm :formData="value" :parentKey="key + '_'" />
                    </div>
                </template>
                <template v-else>
                    <input
                        :type="getFieldType(value)"
                        :id="key"
                        :name="key"
                        v-model="formData[key]" />
                </template>
                <br />
            </template>
            <input type="submit" value="Submit" />
        </form>
    </div>
</template>

<script>
import ObjectForm from "./components/ObjectForm.vue";

export default {
    data() {
        return {
            formData: {
                name: "John Doe",
                age: 25,
                contact: {
                    email: "john.doe@example.com",
                    phone: "123-456-7890",
                    lost: true,
                },
                isSubscribed: true,
                customer: "default",
                config: {
                    passWordHint: "",
                    ticketMailNotification: {
                        status: ["OPEN"],
                        cc: {},
                    },
                    hideTicketTiles: [],
                    ticketExportOptions: {
                        maxRowsToExport: 10000,
                        monthRange: 6,
                    },
                    appName: "",
                    alias: {},
                },
            },
        };
    },
    methods: {
        handleSubmit() {
            // Handle form submission
            console.log(this.formData);
        },
        isObject(obj) {
            return obj !== null && typeof obj === "object";
        },
        getFieldType(value) {
            if (typeof value === "string") {
                return "text";
            } else if (typeof value === "number") {
                return "number";
            } else if (typeof value === "boolean") {
                return "checkbox";
            } else {
                return "text";
            }
        },
    },
    components: { ObjectForm },
};
</script>
