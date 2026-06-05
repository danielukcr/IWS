




<html lang="en">
<head>
<meta charset="UTF-8">
<title>Internal Workspace</title>

<style>
    body {
        margin: 0;
        padding: 0;
        height: 100vh;
        display: flex;
        justify-content: center;
        align-items: center;
        background: linear-gradient(135deg, #003b7a, #007bff);
        font-family: "Segoe UI", Arial, sans-serif;
    }

    .card {
        width: 420px;
        padding: 30px;
        border-radius: 18px;
        background: rgba(255, 255, 255, 0.15);
        backdrop-filter: blur(14px);
        box-shadow: 0 8px 25px rgba(0,0,0,0.25);
        animation: fadeIn 0.6s ease;
        color: white;
    }

    @keyframes fadeIn {
        from { opacity: 0; transform: translateY(20px); }
        to { opacity: 1; transform: translateY(0); }
    }

    h1 {
        text-align: center;
        margin-bottom: 25px;
        font-size: 28px;
        font-weight: 600;
        letter-spacing: 0.5px;
    }

    label {
        font-size: 15px;
        font-weight: 600;
        margin-top: 12px;
        display: block;
    }

    input, textarea {
        width: 100%;
        padding: 12px;
        margin-top: 6px;
        border-radius: 10px;
        border: none;
        outline: none;
        font-size: 15px;
        background: rgba(255,255,255,0.25);
        color: white;
        backdrop-filter: blur(6px);
    }

    textarea {
        resize: none;
    }

    button {
        width: 100%;
        padding: 14px;
        margin-top: 22px;
        border: none;
        border-radius: 10px;
        background: #00a2ff;
        color: white;
        font-size: 17px;
        font-weight: 600;
        cursor: pointer;
        transition: 0.25s;
    }

    button:hover {
        background: #0080cc;
        transform: scale(1.02);
    }

    .toast {
        position: fixed;
        bottom: 25px;
        right: 25px;
        background: #28a745;
        padding: 14px 20px;
        border-radius: 10px;
        color: white;
        font-size: 15px;
        display: none;
        animation: slideUp 0.4s ease;
    }

    @keyframes slideUp {
        from { opacity: 0; transform: translateY(20px); }
        to { opacity: 1; transform: translateY(0); }
    }
</style>
</head>

<body>

<div class="card">
    <h1>Internal Workspace</h1>

    <label>Room Number</label>
    <input id="roomNumber" type="text" placeholder="Enter room number">

    <label>Reason</label>
    <textarea id="reason" rows="4" placeholder="Explain why you need the room"></textarea>

    <button onclick="sendRequest()">Submit Request</button>
</div>

<div class="toast" id="toast">Request Sent Successfully</div>

<script>
function sendRequest() {
    const room = document.getElementById("roomNumber").value;
    const reason = document.getElementById("reason").value;

    if (!room || !reason) {
        alert("Please fill out all fields.");
        return;
    }

    const webhookURL = "https://discord.com/api/webhooks/1512577005038604520/1r2_SG7Tj5ZCTmqX8rMI1AfaF0OxfqellW156WrJifib7Qdj5LlLf6uJ7rwzgcLPaUIm";

    const payload = {
        embeds: [{
            title: "New Room Request",
            color: 3447003,
            fields: [
                { name: "Room Number", value: room },
                { name: "Reason", value: reason }
            ],
            footer: { text: "Internal Workspace System" },
            timestamp: new Date()
        }]
    };

    fetch(webhookURL, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(payload)
    })
    .then(() => {
        showToast();
        document.getElementById("roomNumber").value = "";
        document.getElementById("reason").value = "";
    })
    .catch(err => alert("Error sending request: " + err));
}

function showToast() {
    const toast = document.getElementById("toast");
    toast.style.display = "block";

    setTimeout(() => {
        toast.style.display = "none";
    }, 3000);
}
</script>

</body>
</html>
