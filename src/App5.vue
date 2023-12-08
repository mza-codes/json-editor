<template>
    <json-editor ref="JsonEditor" :schema="schema" v-model="model">
        <button @click="submit">submit</button>
        <button @click="reset">Reset</button>
    </json-editor>
</template>

<script>
const SCHEMA = {
    type: "object",
    title: "vue-json-editor demo",
    properties: {
        name: {
            type: "string",
        },
        email: {
            type: "string",
        },
    },
};
// import vue-json-ui-editor
import JsonEditor from "vue-json-ui-editor";

export default {
    components: { JsonEditor },
    data: () => ({
        // init json schma file ( require('@/schema/newsletter') )
        schema: SCHEMA,
        // data
        model: {
            name: "Yourtion",
        },
    }),

    methods: {
        submit(_e) {
            alert(JSON.stringify(this.model));
        },
        reset() {
            this.$refs.JsonEditor.reset();
        },
    },
};

const sampleJSON = {
    customer: "default",
    config: {
        passWordHint: "",
        ticketMailNotification: { status: ["OPEN"], cc: {} },
        hideTicketTiles: [],
        ticketExportOptions: { maxRowsToExport: 10000, monthRange: 6 },
        appName: "",
        alias: {},
    },
};
</script>
