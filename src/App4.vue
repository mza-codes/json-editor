<template>
    <div>
        <Vue3JsonEditor
            v-model="json"
            :show-btns="true"
            :expandedOnStart="true"
            @json-change="onJsonChange"
            @mode-change="onModeChange" />
    </div>
    <section>
        <pre>
            {{ json }}
        </pre>
    </section>
</template>

<script>
import { defineComponent, reactive, toRefs } from "vue";
import { Vue3JsonEditor } from "vue3-json-editor";

const sampleJSON = {
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
};

export default defineComponent({
    components: {
        Vue3JsonEditor,
    },
    setup() {
        function onJsonChange(value) {
            console.log("value:", value);
        }

        function onModeChange(value) {
            console.log("value:", value);
        }

        const state = reactive({
            json: sampleJSON,
        });

        return {
            ...toRefs(state),
            onJsonChange,
            onModeChange,
        };
    },
});
</script>
