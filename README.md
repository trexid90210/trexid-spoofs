<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>trexid spoofs</title>
    <link rel="icon" href="https://via.placeholder.com/32" type="image/png">
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body, html {
            height: 100%;
            font-family: Arial, sans-serif;
            background: #121212;
            color: white;
        }
        .content {
            text-align: center;
            padding-top: 60px;
        }
        .menu {
            position: absolute;
            top: 20px;
            right: 20px;
            z-index: 10;
        }
        .menu a {
            color: white;
            text-decoration: none;
            padding: 10px;
            margin-left: 10px;
            font-size: 18px;
        }
        .menu a:hover { color: #ffcc00; }
        h1 { font-size: 2rem; margin-top: 20px; }
        input, button {
            padding: 10px;
            margin-top: 20px;
            font-size: 16px;
            border: none;
            border-radius: 5px;
        }
        input { width: 300px; }
        button {
            background-color: #007bff;
            color: white;
            cursor: pointer;
        }
        iframe {
            margin-top: 30px;
            border: none;
            width: 100%;
            height: 600px;
        }
        .hidden { display: none; }
        footer {
            position: fixed;
            bottom: 10px;
            left: 50%;
            transform: translateX(-50%);
            color: white;
        }
        #character {
            position: fixed;
            bottom: 10px;
            right: 10px;
            cursor: pointer;
            z-index: 10;
        }
        #character img {
            width: 70px;
            height: 70px;
        }
        #infoBox {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: rgba(0, 0, 0, 0.85);
            padding: 20px;
            border-radius: 10px;
            color: white;
            z-index: 20;
        }
        #infoBox button {
            margin-top: 15px;
            background-color: #dc3545;
        }
        .tabs {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-top: 30px;
        }
        .tabs button {
            background-color: #333;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 10px;
            cursor: pointer;
        }
        .tabs button:hover {
            background-color: #555;
        }
        #chatWindow {
            position: fixed;
            bottom: 0;
            right: 0;
            width: 320px;
            height: 400px;
            background-color: #fff;
            border-radius: 20px 0 0 20px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
            transform: translateX(100%);
            transition: transform 0.3s ease;
            overflow-y: auto;
            padding: 10px;
        }
        #chatWindow.active {
            transform: translateX(0);
        }
        #chatMessages {
            height: calc(100% - 50px);
            overflow-y: auto;
            color: black;
            padding: 10px;
            background-color: #f4f4f4;
            border-radius: 10px;
        }
        #chatInput {
            padding: 10px;
            width: calc(100% - 20px);
            margin: 10px 0;
            border-radius: 5px;
        }
        .message {
            margin: 10px 0;
            padding: 5px;
            background-color: #e2e2e2;
            border-radius: 5px;
        }
        #chatIcon {
            position: fixed;
            top: 20px;
            right: 130px;
            font-size: 25px;
            cursor: pointer;
            z-index: 15;
        }
    </style>
</head>
<body>
    <div class="content">
        <div class="menu">
            <a href="javascript:void(0)" onclick="openSettings()">⚙️</a>
            <a href="javascript:void(0)" onclick="triggerEmergencyRedirect()">🚨</a>
            <a href="javascript:void(0)" onclick="toggleChatWindow()">💬</a>
        </div>
        <h1>trexid spoofs</h1>
        <div class="tabs">
            <button onclick="openFeaturePanel()">Features</button>
        </div>
        <div id="featurePanel" class="hidden">
            <button onclick="openYouTubeAPI()">YouTube API</button>
            <button onclick="openSpoofs()">Spoofs</button>
            <button onclick="openMovies()">Movies</button>
        </div>
        <div id="youtubeAPI" class="hidden">
            <input id="videoId" type="text" placeholder="Enter YouTube Video ID">
            <button onclick="loadVideo()">Load</button>
            <div id="videoContainer"></div>
        </div>
        <div id="spoofs" class="hidden">
            <p style="margin-top: 30px;">More spoof options coming soon!</p>
        </div>
        <div id="movies" class="hidden">
            <p>Unfortunately, most of the movies don't work. If the movie isn't loading, be patient and refresh the page.</p>
            <p><a href="https://pstream.org/" target="_blank" rel="noopener noreferrer">Click here to open movies</a></p>
        </div>
        <div id="settings" class="hidden">
            <input id="emergencyUrl" type="text" placeholder="Set emergency redirect URL">
        </div>
    </div>
    <footer>
        <p>trexid spoofs - Your go-to tool</p>
    </footer>
    <div id="character" onclick="showInfo()">
        <img src="https://img.icons8.com/emoji/96/smiling-face.png" alt="Smiley">
    </div>
    <div id="infoBox">
        <p>I'm a 15-year-old and I like making websites. Also, I enjoy watching and playing games during class. This website was made by AI and human intelligence.</p>
        <button onclick="hideInfo()">Back</button>
    </div>
    <!-- Chat Window -->
    <div id="chatWindow">
        <div id="chatMessages">
            <div class="message">Hello, this is your personal assistant while using this website. Feel free to ask me anything like, "How was this website made?"</div>
        </div>
        <input type="text" id="chatInput" placeholder="Type your message..." onkeyup="sendMessage(event)">
    </div>

    <script>
        function toggleChatWindow() {
            const chatWindow = document.getElementById('chatWindow');
            const chatInput = document.getElementById('chatInput');
            chatWindow.classList.toggle('active');
            if (chatWindow.classList.contains('active')) chatInput.focus();
        }

        function sendMessage(event) {
            if (event.key === 'Enter') {
                const chatInput = document.getElementById('chatInput');
                const chatMessages = document.getElementById('chatMessages');
                const message = chatInput.value.trim();
                if (message) {
                    const userMessage = document.createElement('div');
                    userMessage.classList.add('message');
                    userMessage.textContent = message;
                    chatMessages.appendChild(userMessage);
                    chatInput.value = '';

                    const assistantMessage = document.createElement('div');
                    assistantMessage.classList.add('message');
                    assistantMessage.textContent = getAssistantResponse(message);
                    chatMessages.appendChild(assistantMessage);

                    chatMessages.scrollTop = chatMessages.scrollHeight;
                }
            }
        }

        function getAssistantResponse(userMessage) {
            const lowerMessage = userMessage.toLowerCase();
            if (lowerMessage.includes('how') || lowerMessage.includes('website')) {
                return "This website was created with HTML, CSS, and JavaScript—plus a bit of AI magic!";
            } else if (lowerMessage.includes('hello')) {
                return "Hi there! What would you like to explore today?";
            } else if (lowerMessage.includes('bye')) {
                return "Goodbye! Hope to see you again soon.";
            } else {
                return "That's interesting! Tell me more or ask something else.";
            }
        }

        function loadVideo() {
            const input = document.getElementById("videoId").value.trim();
            const id = input.includes("youtube.com") ? new URL(input).searchParams.get("v") : input;
            const videoContainer = document.getElementById("videoContainer");
            if (id) {
                videoContainer.innerHTML = `<iframe src="https://www.youtube.com/embed/${id}" allowfullscreen></iframe>`;
            } else {
                videoContainer.innerHTML = '<p>Invalid video ID or URL</p>';
            }
        }

        function openYouTubeAPI() {
            toggleView("youtubeAPI");
        }

        function openSpoofs() {
            toggleView("spoofs");
        }

        function openMovies() {
            toggleView("movies");
        }

        function openSettings() {
            toggleView("settings");
        }

        function openFeaturePanel() {
            toggleView("featurePanel");
        }

        function toggleView(sectionId) {
            const sections = ["youtubeAPI", "spoofs", "settings", "movies", "featurePanel"];
            sections.forEach(id => document.getElementById(id).classList.add("hidden"));
            document.getElementById(sectionId).classList.remove("hidden");
        }

        function showInfo() {
            document.getElementById("infoBox").style.display = "block";
        }

        function hideInfo() {
            document.getElementById("infoBox").style.display = "none";
        }

        function triggerEmergencyRedirect() {
            const emergencyUrl = document.getElementById("emergencyUrl").value;
            if (emergencyUrl) {
                window.location.href = emergencyUrl;
            } else {
                alert("Please set the emergency URL first.");
            }
        }
    </script>
</body>
</html>
