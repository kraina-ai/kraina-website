<script>

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
        alert("Form submitted successfully");
    } else {
        console.error('Error:', response.statusText);
    }
}

</script>
