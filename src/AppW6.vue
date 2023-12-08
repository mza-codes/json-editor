<script>
import JsonEditorVue from "json-editor-vue";

export default {
    name: "fdUI",
    data() {
        return {
            value: {
                data: [1, 4, 5, 2, 0],
                power: "like",
                alias: {
                    ticket: "dsf",
                    exportconf: {
                        name: 4,
                        id: "44",
                        restOpts: {
                            P: 90,
                        },
                    },
                },
            },
        };
    },
    components: { JsonEditorVue },
};
</script>

<template>
    <main class="parent">
        <section>
            <JsonEditorVue
                v-model="value"
                v-bind="{
                    /* local props & attrs */
                }" />
        </section>

        <pre>
            {{ value }}
        </pre>
    </main>
</template>
<style>
.parent {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
}
.parent > * {
    flex: 1;
}
</style>
