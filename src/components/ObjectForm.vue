<template>
    <div>
        <template v-for="(value, key) in formData" :key="key">
            <label :for="parentKey + key">{{ parentKey + key }}:</label>
            <template v-if="isArray(value)"> "Array found here" => {{ value }} </template>
            <template v-if="isObject(value)">
                <ObjectForm :formData="value" :parentKey="parentKey + key + '_'" />
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
    name: "ObjectForm",
    props: {
        formData: Object,
        parentKey: String,
    },
    methods: {
        isObject(obj) {
            return obj !== null && typeof obj === "object";
        },
        isArray(value) {
            let r = value instanceof Array;
            // if (!r) r = value?.length >= 0;
            return r;
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
