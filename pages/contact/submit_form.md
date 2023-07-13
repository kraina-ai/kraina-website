<script>

const _ERROR_MESSAGE = "Something went wrong.";
const _SUCCESS_MESSAGE = "Thank you for contacting us! We will get back to you as soon as possible.";

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

    const response = await fetch('http://localhost:8080/endpoint', {
        method: 'POST', 
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify(formData)
    });

    if (response.ok) {
        const jsonResponse = await response.json();
        console.log(jsonResponse);
        form.reset();
        alert(_SUCCESS_MESSAGE);
    } else {
        alert(_ERROR_MESSAGE + response.statusText + ".");
        console.error("Error:", response.statusText);
    }
}

</script>
