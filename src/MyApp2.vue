<template>
    <div id="form-container"></div>
</template>

<script>
export default {
    mounted() {
        // Example nested JSON object
        const exampleJson = {
            name: "John Doe",
            age: 25,
            contact: {
                email: "john.doe@example.com",
                phone: "123-456-7890",
            },
            isSubscribed: true,
        };

        // Call the function with the nested JSON object
        jsonToForm(exampleJson);
    },
};
function jsonToForm(jsonObject, parentKey = "") {
    const formContainer = document.getElementById("form-container");
    let formHTML = "<form>";
    const objects = [];

    for (const key in jsonObject) {
        // eslint-disable-next-line
        if (jsonObject.hasOwnProperty(key)) {
            const nestedKey = parentKey ? parentKey + "_" + key : key;

            formHTML += '<label for="' + nestedKey + '">' + nestedKey + ":</label>";

            if (typeof jsonObject[key] === "object" && jsonObject[key] !== null) {
                // Recursively handle nested objects
                objects.push({ object: jsonObject[key], nestedKey });
            } else {
                // Handle primitive types
                formHTML += generateFormField(nestedKey, jsonObject[key]);
            }

            formHTML += "<br>";
        }
    }

    objects.forEach((v) => {
        const r = jsonToForm(...Object.values(v));
    });

    formHTML += '<input type="submit" value="Submit"></form>';
    formContainer.innerHTML = formHTML;
}

function generateFormField(key, value) {
    if (typeof value === "string") {
        return (
            '<input type="text" id="' +
            key +
            '" name="' +
            key +
            '" value="' +
            value +
            '">'
        );
    } else if (typeof value === "number") {
        return (
            '<input type="number" id="' +
            key +
            '" name="' +
            key +
            '" value="' +
            value +
            '">'
        );
    } else if (typeof value === "boolean") {
        return (
            '<input type="checkbox" id="' +
            key +
            '" name="' +
            key +
            '" ' +
            (value ? "checked" : "") +
            ">"
        );
    } else {
        // Handle other types as needed
        return (
            '<input type="text" id="' +
            key +
            '" name="' +
            key +
            '" value="' +
            value +
            '">'
        );
    }
}
</script>
