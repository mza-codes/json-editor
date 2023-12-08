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
    <JsonEditorVue
        v-model="value"
        v-bind="{
            /* local props & attrs */
        }" />

    <section>
        <pre>
            {{ value }}
          </pre
        >
    </section>
</template>
<style>
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}
</style>
