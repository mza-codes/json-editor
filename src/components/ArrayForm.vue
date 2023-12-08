<template>
    <div>
        <template v-for="(value, key) in formData" :key="key">
            <label :for="parentKey + key">{{ parentKey + key }}:</label>
            <template v-if="isArray(value)">
                <ArrayForm :formData="value" :parentKey="parentKey + key + '_'" />
            </template>
            <template v-else>
                <input
                    :type="getFieldType(value)"
                    :id="parentKey + key"
                    :name="parentKey + key"
                    v-model="formField[key]" />
            </template>
            <br />
        </template>
    </div>
</template>

<script>
export default {
    name: "ArrayForm",
    props: {
        formData: Object,
        parentKey: String,
    },
    methods: {
        isArray(obj) {
            if (obj instanceof Array) {
                console.log("OBJ is Array", { obj });
                return true;
            }
            return false;
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
    computed: {
        formField() {
            return this.formData;
        },
    },
};
</script>
