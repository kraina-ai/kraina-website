<script>

const _ERROR_MESSAGE = "Something went wrong.";
const _SUCCESS_MESSAGE = "Thank you for contacting us! We will get back to you as soon as possible.";
const _ENDPOINT = "https://tejc4zjnbzyt77cyhzl62k2afi0hobae.lambda-url.eu-north-1.on.aws/";

async function submit() {
    const form = document.getElementById("form");
    const name_field = form.elements["nameField"];
    const email_field = form.elements["emailField"];
    const subject_field = form.elements["subjectField"];
    const message_field = form.elements["messageField"];

    const formData = {
        name: name_field.value,
        email: email_field.value,
        subject: subject_field.value,
        message: message_field.value
    };

    try {
        const response = await fetch(_ENDPOINT, {
            method: 'POST', 
            headers: {
                'Content-Type': 'application/json',
            },
            body: JSON.stringify(formData)
        });
        await handleResponse(response);
    }
    catch (error) {
        showError(error);
    }
}

async function handleResponse(response) {
    if (response.ok) {
        const textResponse = await response.text();
        console.log(textResponse);
        alert(_SUCCESS_MESSAGE);
        form.reset();
    } else {
        showError(response.statusText);
    }
}

function showError(additionalInfo) {
    alert(_ERROR_MESSAGE);
    console.error("Error:", additionalInfo);
}

</script>
