<template>
    <div id="form-container"></div>
</template>

<script>
const sampleJSON = {
    customer: "blinkitapp",
    domainWhitelist: [
        "gipltp.com",
        "grofers.com",
        "ext.grofers.com",
        "zomato.com",
        "blinkit.com",
        "gallervigilate.com",
    ],
    config: {
        passWordHint: "Default Password is set to your Phone number",
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
        loginMethods: {
            otp: false,
            sso: true,
            credentials: false,
        },
        helpline: "+91 8588876425",
        alias: {
            asset: {
                title: "Store",
            },
            ticket: {
                title: "Task",
                exportVisibleColumnsOnly: false,
                exportConfig: {
                    ticketId: "taskId",
                    location: "Store",
                    locationId: "StoreId",
                    title: "summary",
                    "description.text": "description",
                    event: "Issue Type",
                    subEvent: "Issue SubType",
                    eventDate: "Happened Date",
                    dueDate: "Due Date",
                    createdBy: "createdBy",
                    assignedTo: "assignedTo",
                    priority: "Priority",
                    status: "Status",
                    onHold: "onHold",
                    "additionalInformation.preVisit": "PreVisitList",
                    "additionalInformation.postVisit": "PostVisitList",
                    "additionalInformation.vendor": "vendor",
                    id: "url",
                },
                importConfig: {
                    excludedKeys: {
                        type: "TICKET",
                        entityId: null,
                        entityType: "EQUIPMENT",
                        acknowledged: false,
                        metadata: {},
                        attachments: [],
                        "additionalInformation.assetLabel": "",
                        "additionalInformation.assignedToAdmin": false,
                    },
                    dataFormats: {
                        onHold: {
                            type: "Boolean",
                        },
                        "additionalInformation.preVisit": {
                            type: "ArrayObject",
                            split: ",",
                        },
                        "additionalInformation.postVisit": {
                            type: "ArrayObject",
                            split: ",",
                        },
                    },
                },
            },
            ticketStatus: {},
        },
    },
    sellerConfig: {
        logo: "/static/blinkitapp/galler.svg",
        name: "galler",
    },
};

export default {
    data: () => ({
        formEl: undefined,
    }),
    mounted() {
        const exampleJson = {
            name: "John Doe",
            age: 25,
            email: "john.doe@example.com",
            isSubscribed: true,
            Powe: "John Doe",
            address: {
                street: "123 Main St",
                city: "Example City",
            },
            hobbies: ["Reading", "Coding"],
        };
        this.formEl = document.getElementById("form-container");
        jsonToForm(sampleJSON);
    },
    methods: {
        submitForm(...args) {
            console.log("@submit", { args });
        },
        jsonToForm(jsonObject) {
            const formContainer = document.getElementById("form-container");
            let formHTML = "<form>";

            formHTML += '<input @click="submitForm" type="submit" value="Submit"></form>';
            formContainer.innerHTML = formHTML;
        },
        generateFields(jsonObject) {
            let formHTML = ``;
            for (const key in jsonObject) {
                // eslint-disable-next-line
                if (jsonObject.hasOwnProperty(key)) {
                    formHTML += '<label for="' + key + '">' + key + ":</label>";

                    // Check the type of the value to determine the appropriate form field
                    if (typeof jsonObject[key] === "string") {
                        formHTML +=
                            '<input type="text" id="' +
                            key +
                            '" name="' +
                            key +
                            '" value="' +
                            jsonObject[key] +
                            '">';
                    } else if (typeof jsonObject[key] === "number") {
                        formHTML +=
                            '<input type="number" id="' +
                            key +
                            '" name="' +
                            key +
                            '" value="' +
                            jsonObject[key] +
                            '">';
                    } else if (typeof jsonObject[key] === "boolean") {
                        formHTML +=
                            '<input type="checkbox" id="' +
                            key +
                            '" name="' +
                            key +
                            '" ' +
                            (jsonObject[key] ? "checked" : "") +
                            ">";
                    } else if (typeof jsonObject[key] === "object") {
                        const res = this.generateFields(jsonObject[key]);
                        formHTML += res;
                        // formHTML += `<input type="text" id="${key}" name="${key}" value="${jsonObject[key]}">`;
                    } else {
                        // Handle other types as needed
                        formHTML +=
                            '<input type="text" id="' +
                            key +
                            '" name="' +
                            key +
                            '" value="' +
                            jsonObject[key] +
                            '">';
                    }

                    formHTML += "<br>";
                }
            }
            return formHTML;
        },
    },
};
function jsonToForm(jsonObject) {
    const formContainer = document.getElementById("form-container");
    let formHTML = "<form>";

    for (const key in jsonObject) {
        // eslint-disable-next-line
        if (jsonObject.hasOwnProperty(key)) {
            formHTML += '<label for="' + key + '">' + key + ":</label>";

            // Check the type of the value to determine the appropriate form field
            if (typeof jsonObject[key] === "string") {
                formHTML +=
                    '<input type="text" id="' +
                    key +
                    '" name="' +
                    key +
                    '" value="' +
                    jsonObject[key] +
                    '">';
            } else if (typeof jsonObject[key] === "number") {
                formHTML +=
                    '<input type="number" id="' +
                    key +
                    '" name="' +
                    key +
                    '" value="' +
                    jsonObject[key] +
                    '">';
            } else if (typeof jsonObject[key] === "boolean") {
                formHTML +=
                    '<input type="checkbox" id="' +
                    key +
                    '" name="' +
                    key +
                    '" ' +
                    (jsonObject[key] ? "checked" : "") +
                    ">";
            } else if (typeof jsonObject[key] === "object") {
                const res = generateNestedFormFromObject(jsonObject[key]);
                if (res) {
                    formHTML += ``;
                }
                // formHTML += `<input type="text" id="${key}" name="${key}" value="${jsonObject[key]}">`;
            } else {
                // Handle other types as needed
                formHTML +=
                    '<input type="text" id="' +
                    key +
                    '" name="' +
                    key +
                    '" value="' +
                    jsonObject[key] +
                    '">';
            }

            formHTML += "<br>";
        }
    }

    formHTML += '<input @click="submitForm" type="submit" value="Submit"></form>';
    formContainer.innerHTML = formHTML;
}
/**@param {Record<string, any>} form */
function generateNestedFormFromObject(form) {
    const isEmpty = Object.values(form).length <= 0;
    if (isEmpty) return null;
    const returnArr = [];
    return returnArr;
}
</script>
