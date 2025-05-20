<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Entrepreneur Mentor AI - Vidya & Vichaar</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap');
        
        body {
            font-family: 'Poppins', sans-serif;
            background-color: #f0f7ff;
        }
        
        .chat-container {
            height: calc(100vh - 120px);
            scrollbar-width: thin;
            scrollbar-color: #4f46e5 #e0e7ff;
        }
        
        .chat-container::-webkit-scrollbar {
            width: 6px;
        }
        
        .chat-container::-webkit-scrollbar-track {
            background: #e0e7ff;
        }
        
        .chat-container::-webkit-scrollbar-thumb {
            background-color: #4f46e5;
            border-radius: 20px;
        }
        
        .vidya-bubble {
            background: linear-gradient(135deg, #6366f1 0%, #8b5cf6 100%);
            color: white;
            border-radius: 20px 20px 20px 0;
        }
        
        .vichaar-bubble {
            background: linear-gradient(135deg, #10b981 0%, #3b82f6 100%);
            color: white;
            border-radius: 20px 20px 0 20px;
        }
        
        .user-bubble {
            background-color: #e0e7ff;
            border-radius: 20px 20px 0 20px;
        }
        
        .typing-indicator span {
            display: inline-block;
            width: 8px;
            height: 8px;
            border-radius: 50%;
            background-color: #4f46e5;
            margin: 0 2px;
            animation: bounce 1.4s infinite ease-in-out;
        }
        
        .typing-indicator span:nth-child(2) {
            animation-delay: 0.2s;
        }
        
        .typing-indicator span:nth-child(3) {
            animation-delay: 0.4s;
        }
        
        @keyframes bounce {
            0%, 60%, 100% { transform: translateY(0); }
            30% { transform: translateY(-8px); }
        }
        
        .character-selector {
            transition: all 0.3s ease;
        }
        
        .character-selector:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
        }
        
        .character-selected {
            border: 3px solid #4f46e5;
            box-shadow: 0 0 0 4px rgba(79, 70, 229, 0.2);
        }
        
        .model-viewer {
            transition: all 0.5s ease;
        }
        
        .model-viewer:hover {
            transform: scale(1.02);
        }
        
        .language-selector {
            background: rgba(255, 255, 255, 0.2);
            backdrop-filter: blur(10px);
        }
    </style>
</head>
<body class="bg-gray-50">
    <!-- Header -->
    <header class="bg-gradient-to-r from-indigo-600 to-purple-600 text-white shadow-lg">
        <div class="container mx-auto px-4 py-6">
            <div class="flex justify-between items-center">
                <div class="flex items-center space-x-3">
                    <div class="bg-white p-2 rounded-full">
                        <i class="fas fa-lightbulb text-indigo-600 text-2xl"></i>
                    </div>
                    <h1 class="text-2xl font-bold">Entrepreneur Mentor AI</h1>
                </div>
                <div class="relative">
                    <button id="languageBtn" class="bg-white text-indigo-600 px-4 py-2 rounded-full font-medium flex items-center space-x-2">
                        <i class="fas fa-globe"></i>
                        <span>English</span>
                        <i class="fas fa-chevron-down text-xs"></i>
                    </button>
                    <div id="languageDropdown" class="language-selector absolute right-0 mt-2 w-48 rounded-md shadow-lg hidden z-50">
                        <div class="py-1">
                            <a href="#" class="block px-4 py-2 text-sm text-gray-700 hover:bg-indigo-100">English</a>
                            <a href="#" class="block px-4 py-2 text-sm text-gray-700 hover:bg-indigo-100">हिन्दी (Hindi)</a>
                            <a href="#" class="block px-4 py-2 text-sm text-gray-700 hover:bg-indigo-100">தமிழ் (Tamil)</a>
                            <a href="#" class="block px-4 py-2 text-sm text-gray-700 hover:bg-indigo-100">తెలుగు (Telugu)</a>
                            <a href="#" class="block px-4 py-2 text-sm text-gray-700 hover:bg-indigo-100">മലയാളം (Malayalam)</a>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </header>

    <!-- Main Content -->
    <main class="container mx-auto px-4 py-6">
        <!-- Character Selection -->
        <div id="characterSelection" class="mb-8">
            <h2 class="text-2xl font-bold text-gray-800 mb-6 text-center">Choose Your Mentor</h2>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
                <div id="vidyaOption" class="character-selector bg-white p-6 rounded-xl shadow-md cursor-pointer transition-all duration-300 hover:shadow-lg">
                    <div class="flex flex-col items-center text-center">
                        <div class="w-32 h-32 bg-indigo-100 rounded-full flex items-center justify-center mb-4">
                            <img src="https://img.icons8.com/color/96/000000/teacher.png" alt="Vidya" class="w-20 h-20">
                        </div>
                        <h3 class="text-xl font-bold text-indigo-700 mb-2">Vidya</h3>
                        <p class="text-gray-600 mb-4">The Knowledge Mentor</p>
                        <p class="text-gray-700">Analyzes your skills, education, and goals to provide personalized career guidance and identify suitable government schemes.</p>
                        <button id="selectVidya" class="mt-4 bg-indigo-600 text-white px-6 py-2 rounded-full font-medium hover:bg-indigo-700 transition">Select Vidya</button>
                    </div>
                </div>
                <div id="vichaarOption" class="character-selector bg-white p-6 rounded-xl shadow-md cursor-pointer transition-all duration-300 hover:shadow-lg">
                    <div class="flex flex-col items-center text-center">
                        <div class="w-32 h-32 bg-green-100 rounded-full flex items-center justify-center mb-4">
                            <img src="https://img.icons8.com/color/96/000000/idea.png" alt="Vichaar" class="w-20 h-20">
                        </div>
                        <h3 class="text-xl font-bold text-green-700 mb-2">Vichaar</h3>
                        <p class="text-gray-600 mb-4">The Creative Ideator</p>
                        <p class="text-gray-700">Generates innovative business ideas tailored to your profile and creates 3D visual mockups of your potential startup concept.</p>
                        <button id="selectVichaar" class="mt-4 bg-green-600 text-white px-6 py-2 rounded-full font-medium hover:bg-green-700 transition">Select Vichaar</button>
                    </div>
                </div>
            </div>
        </div>

        <!-- Chat Interface (Initially Hidden) -->
        <div id="chatInterface" class="hidden">
            <div class="bg-white rounded-xl shadow-xl overflow-hidden">
                <!-- Chat Header -->
                <div class="bg-gradient-to-r from-indigo-600 to-purple-600 p-4 flex items-center justify-between">
                    <div class="flex items-center space-x-3">
                        <div id="characterAvatar" class="w-12 h-12 bg-white rounded-full flex items-center justify-center">
                            <i id="characterIcon" class="text-2xl"></i>
                        </div>
                        <div>
                            <h2 id="characterName" class="text-white font-bold text-lg"></h2>
                            <p id="characterRole" class="text-indigo-100 text-sm"></p>
                        </div>
                    </div>
                    <button id="backToSelection" class="text-white hover:text-indigo-200">
                        <i class="fas fa-arrow-left"></i> Back
                    </button>
                </div>
                
                <!-- Chat Messages -->
                <div id="chatContainer" class="chat-container p-4 overflow-y-auto">
                    <div id="welcomeMessage" class="mb-4">
                        <div class="flex items-start space-x-2">
                            <div id="characterAvatarSmall" class="w-8 h-8 bg-indigo-100 rounded-full flex items-center justify-center mt-1">
                                <i id="characterIconSmall" class="text-indigo-600 text-sm"></i>
                            </div>
                            <div class="vidya-bubble px-4 py-3 max-w-xs md:max-w-md lg:max-w-lg">
                                <p id="welcomeText" class="text-white"></p>
                            </div>
                        </div>
                    </div>
                </div>
                
                <!-- User Input -->
                <div class="border-t border-gray-200 p-4 bg-gray-50">
                    <div class="flex items-center space-x-2">
                        <input id="userInput" type="text" placeholder="Type your message here..." class="flex-1 border border-gray-300 rounded-full px-4 py-2 focus:outline-none focus:ring-2 focus:ring-indigo-500">
                        <button id="sendButton" class="bg-indigo-600 text-white p-2 rounded-full hover:bg-indigo-700 transition">
                            <i class="fas fa-paper-plane"></i>
                        </button>
                        <button id="voiceButton" class="bg-white text-indigo-600 p-2 rounded-full border border-indigo-600 hover:bg-indigo-50 transition">
                            <i class="fas fa-microphone"></i>
                        </button>
                    </div>
                    <div class="mt-2 text-xs text-gray-500 text-center">
                        <p>Press Enter to send or click the microphone to speak</p>
                    </div>
                </div>
            </div>
        </div>

        <!-- 3D Model Viewer (Initially Hidden) -->
        <div id="modelViewer" class="hidden mt-8 bg-white rounded-xl shadow-xl overflow-hidden">
            <div class="bg-gradient-to-r from-green-600 to-blue-600 p-4 text-white">
                <h2 class="text-lg font-bold flex items-center">
                    <i class="fas fa-cube mr-2"></i> 3D Concept Visualization by Vichaar
                </h2>
            </div>
            <div class="p-4">
                <div class="model-viewer bg-gray-100 rounded-lg h-64 md:h-96 flex items-center justify-center">
                    <div id="modelPlaceholder" class="text-center p-6">
                        <i class="fas fa-cube text-5xl text-gray-400 mb-4"></i>
                        <h3 class="text-xl font-bold text-gray-600 mb-2">Your 3D Concept</h3>
                        <p class="text-gray-500">Vichaar will generate a 3D visualization of your business idea here.</p>
                    </div>
                    <canvas id="modelCanvas" class="hidden w-full h-full"></canvas>
                </div>
                <div class="mt-4 flex justify-between">
                    <button id="rotateModel" class="bg-gray-200 text-gray-700 px-4 py-2 rounded hover:bg-gray-300">
                        <i class="fas fa-sync-alt mr-2"></i> Rotate
                    </button>
                    <button id="downloadModel" class="bg-green-600 text-white px-4 py-2 rounded hover:bg-green-700">
                        <i class="fas fa-download mr-2"></i> Download
                    </button>
                </div>
            </div>
        </div>
    </main>

    <!-- Footer -->
    <footer class="bg-gray-800 text-white py-8">
        <div class="container mx-auto px-4">
            <div class="flex flex-col md:flex-row justify-between items-center">
                <div class="mb-4 md:mb-0">
                    <h2 class="text-xl font-bold flex items-center">
                        <i class="fas fa-lightbulb mr-2 text-indigo-400"></i> Entrepreneur Mentor AI
                    </h2>
                    <p class="text-gray-400 mt-1">Empowering the next generation of innovators</p>
                </div>
                <div class="flex space-x-6">
                    <a href="#" class="text-gray-400 hover:text-white">
                        <i class="fab fa-facebook-f"></i>
                    </a>
                    <a href="#" class="text-gray-400 hover:text-white">
                        <i class="fab fa-twitter"></i>
                    </a>
                    <a href="#" class="text-gray-400 hover:text-white">
                        <i class="fab fa-linkedin-in"></i>
                    </a>
                    <a href="#" class="text-gray-400 hover:text-white">
                        <i class="fab fa-instagram"></i>
                    </a>
                </div>
            </div>
            <div class="border-t border-gray-700 mt-6 pt-6 text-center text-gray-400 text-sm">
                <p>© 2023 Entrepreneur Mentor AI. All rights reserved. | Patent Pending</p>
            </div>
        </div>
    </footer>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            // Language selector toggle
            const languageBtn = document.getElementById('languageBtn');
            const languageDropdown = document.getElementById('languageDropdown');
            
            languageBtn.addEventListener('click', function() {
                languageDropdown.classList.toggle('hidden');
            });
            
            // Close language dropdown when clicking outside
            document.addEventListener('click', function(event) {
                if (!languageBtn.contains(event.target) && !languageDropdown.contains(event.target)) {
                    languageDropdown.classList.add('hidden');
                }
            });
            
            // Character selection
            const characterSelection = document.getElementById('characterSelection');
            const chatInterface = document.getElementById('chatInterface');
            const vidyaOption = document.getElementById('vidyaOption');
            const vichaarOption = document.getElementById('vichaarOption');
            const selectVidya = document.getElementById('selectVidya');
            const selectVichaar = document.getElementById('selectVichaar');
            const backToSelection = document.getElementById('backToSelection');
            
            const characterAvatar = document.getElementById('characterAvatar');
            const characterIcon = document.getElementById('characterIcon');
            const characterName = document.getElementById('characterName');
            const characterRole = document.getElementById('characterRole');
            const characterAvatarSmall = document.getElementById('characterAvatarSmall');
            const characterIconSmall = document.getElementById('characterIconSmall');
            const welcomeText = document.getElementById('welcomeText');
            const modelViewer = document.getElementById('modelViewer');
            
            selectVidya.addEventListener('click', function() {
                // Update UI for Vidya
                characterSelection.classList.add('hidden');
                chatInterface.classList.remove('hidden');
                modelViewer.classList.add('hidden');
                
                characterAvatar.className = 'w-12 h-12 bg-indigo-100 rounded-full flex items-center justify-center';
                characterIcon.className = 'fas fa-chalkboard-teacher text-indigo-600 text-2xl';
                characterName.textContent = 'Vidya';
                characterRole.textContent = 'Knowledge Mentor';
                
                characterAvatarSmall.className = 'w-8 h-8 bg-indigo-100 rounded-full flex items-center justify-center mt-1';
                characterIconSmall.className = 'fas fa-chalkboard-teacher text-indigo-600 text-sm';
                
                welcomeText.textContent = 'Hello! I\'m Vidya, your knowledge mentor. I can help analyze your skills, education, and goals to guide you toward the right entrepreneurial path. Tell me about yourself - your background, skills, and what kind of business you\'re interested in.';
                
                // Highlight selected character
                vidyaOption.classList.add('character-selected');
                vichaarOption.classList.remove('character-selected');
            });
            
            selectVichaar.addEventListener('click', function() {
                // Update UI for Vichaar
                characterSelection.classList.add('hidden');
                chatInterface.classList.remove('hidden');
                modelViewer.classList.remove('hidden');
                
                characterAvatar.className = 'w-12 h-12 bg-green-100 rounded-full flex items-center justify-center';
                characterIcon.className = 'fas fa-lightbulb text-green-600 text-2xl';
                characterName.textContent = 'Vichaar';
                characterRole.textContent = 'Creative Ideator';
                
                characterAvatarSmall.className = 'w-8 h-8 bg-green-100 rounded-full flex items-center justify-center mt-1';
                characterIconSmall.className = 'fas fa-lightbulb text-green-600 text-sm';
                
                welcomeText.textContent = 'Namaste! I\'m Vichaar, your creative ideator. I specialize in generating innovative business ideas tailored just for you and visualizing them in 3D. Share with me your interests, skills, or any business ideas you already have, and I\'ll help bring them to life!';
                
                // Highlight selected character
                vichaarOption.classList.add('character-selected');
                vidyaOption.classList.remove('character-selected');
            });
            
            backToSelection.addEventListener('click', function() {
                characterSelection.classList.remove('hidden');
                chatInterface.classList.add('hidden');
                modelViewer.classList.add('hidden');
                
                // Remove highlights
                vidyaOption.classList.remove('character-selected');
                vichaarOption.classList.remove('character-selected');
                
                // Clear chat
                clearChat();
            });
            
            // Chat functionality
            const chatContainer = document.getElementById('chatContainer');
            const userInput = document.getElementById('userInput');
            const sendButton = document.getElementById('sendButton');
            const voiceButton = document.getElementById('voiceButton');
            
            sendButton.addEventListener('click', sendMessage);
            userInput.addEventListener('keypress', function(e) {
                if (e.key === 'Enter') {
                    sendMessage();
                }
            });
            
            function sendMessage() {
                const message = userInput.value.trim();
                if (message === '') return;
                
                // Add user message to chat
                addMessage(message, 'user');
                userInput.value = '';
                
                // Show typing indicator
                showTypingIndicator();
                
                // Simulate AI response after a delay
                setTimeout(() => {
                    // Remove typing indicator
                    removeTypingIndicator();
                    
                    // Generate AI response based on selected character
                    const isVidya = characterName.textContent === 'Vidya';
                    const aiResponse = generateAIResponse(message, isVidya);
                    
                    // Add AI response to chat
                    addMessage(aiResponse.text, isVidya ? 'vidya' : 'vichaar');
                    
                    // If Vichaar and the response includes a 3D concept, update the model viewer
                    if (!isVidya && aiResponse.hasModel) {
                        updateModelViewer(aiResponse.modelDescription);
                    }
                }, 1500);
            }
            
            function addMessage(text, sender) {
                const messageDiv = document.createElement('div');
                messageDiv.className = 'mb-4';
                
                const messageContent = document.createElement('div');
                messageContent.className = 'flex items-start space-x-2';
                
                if (sender === 'user') {
                    messageContent.innerHTML = `
                        <div class="flex-1"></div>
                        <div class="user-bubble px-4 py-3 max-w-xs md:max-w-md lg:max-w-lg">
                            <p class="text-gray-800">${text}</p>
                        </div>
                        <div class="w-8 h-8 bg-indigo-100 rounded-full flex items-center justify-center mt-1">
                            <i class="fas fa-user text-indigo-600 text-sm"></i>
                        </div>
                    `;
                } else if (sender === 'vidya') {
                    messageContent.innerHTML = `
                        <div class="w-8 h-8 bg-indigo-100 rounded-full flex items-center justify-center mt-1">
                            <i class="fas fa-chalkboard-teacher text-indigo-600 text-sm"></i>
                        </div>
                        <div class="vidya-bubble px-4 py-3 max-w-xs md:max-w-md lg:max-w-lg">
                            <p class="text-white">${text}</p>
                        </div>
                    `;
                } else { // vichaar
                    messageContent.innerHTML = `
                        <div class="w-8 h-8 bg-green-100 rounded-full flex items-center justify-center mt-1">
                            <i class="fas fa-lightbulb text-green-600 text-sm"></i>
                        </div>
                        <div class="vichaar-bubble px-4 py-3 max-w-xs md:max-w-md lg:max-w-lg">
                            <p class="text-white">${text}</p>
                        </div>
                    `;
                }
                
                messageDiv.appendChild(messageContent);
                chatContainer.appendChild(messageDiv);
                
                // Scroll to bottom
                chatContainer.scrollTop = chatContainer.scrollHeight;
            }
            
            function showTypingIndicator() {
                const typingDiv = document.createElement('div');
                typingDiv.className = 'mb-4';
                typingDiv.id = 'typingIndicator';
                
                const typingContent = document.createElement('div');
                typingContent.className = 'flex items-start space-x-2';
                
                const isVidya = characterName.textContent === 'Vidya';
                
                typingContent.innerHTML = `
                    <div class="w-8 h-8 ${isVidya ? 'bg-indigo-100' : 'bg-green-100'} rounded-full flex items-center justify-center mt-1">
                        <i class="${isVidya ? 'fas fa-chalkboard-teacher text-indigo-600' : 'fas fa-lightbulb text-green-600'} text-sm"></i>
                    </div>
                    <div class="bg-gray-200 px-4 py-3 rounded-full">
                        <div class="typing-indicator">
                            <span></span>
                            <span></span>
                            <span></span>
                        </div>
                    </div>
                `;
                
                typingDiv.appendChild(typingContent);
                chatContainer.appendChild(typingDiv);
                
                // Scroll to bottom
                chatContainer.scrollTop = chatContainer.scrollHeight;
            }
            
            function removeTypingIndicator() {
                const typingIndicator = document.getElementById('typingIndicator');
                if (typingIndicator) {
                    typingIndicator.remove();
                }
            }
            
            function generateAIResponse(userMessage, isVidya) {
                // This is a simplified simulation - in a real app, this would call an API
                const responses = {
                    vidya: [
                        {
                            text: "Based on your skills in agriculture, I recommend exploring organic farming with government subsidies. The Paramparagat Krishi Vikas Yojana scheme provides financial assistance for organic farming practices.",
                            hasModel: false
                        },
                        {
                            text: "Your background in computer science is valuable! Have you considered developing educational apps for rural schools? The Startup India scheme offers funding for tech innovations in education.",
                            hasModel: false
                        },
                        {
                            text: "For someone with your textile skills, handloom and handicraft businesses could be profitable. The Mudra Yojana provides loans up to ₹10 lakh for such ventures without collateral.",
                            hasModel: false
                        }
                    ],
                    vichaar: [
                        {
                            text: "Inspired by your love for cooking, how about a cloud kitchen specializing in regional cuisine? I've visualized a modern kitchen space with efficient workflow. Check the 3D model!",
                            hasModel: true,
                            modelDescription: "Cloud kitchen with cooking stations, packaging area, and delivery management zone"
                        },
                        {
                            text: "Your idea for eco-friendly packaging is brilliant! I've created a 3D concept of biodegradable containers made from agricultural waste. The design includes your logo and branding elements.",
                            hasModel: true,
                            modelDescription: "Eco-friendly packaging products with custom branding"
                        },
                        {
                            text: "A mobile app connecting local artisans with global customers? Fantastic! Here's a 3D mockup of the app interface showing product listings, chat features, and secure payment options.",
                            hasModel: true,
                            modelDescription: "Mobile app UI for artisan marketplace"
                        }
                    ]
                };
                
                // Simple keyword matching for demo purposes
                const keywords = {
                    agriculture: 0,
                    computer: 1,
                    textile: 2,
                    cooking: 0,
                    packaging: 1,
                    artisan: 2
                };
                
                let responseIndex = 0;
                for (const [keyword, index] of Object.entries(keywords)) {
                    if (userMessage.toLowerCase().includes(keyword)) {
                        responseIndex = index;
                        break;
                    }
                }
                
                return isVidya ? responses.vidya[responseIndex] : responses.vichaar[responseIndex];
            }
            
            function updateModelViewer(description) {
                const modelPlaceholder = document.getElementById('modelPlaceholder');
                const modelCanvas = document.getElementById('modelCanvas');
                
                // In a real app, this would render an actual 3D model
                // For demo, we'll just show a placeholder with the description
                modelPlaceholder.innerHTML = `
                    <i class="fas fa-cube text-5xl text-green-400 mb-4"></i>
                    <h3 class="text-xl font-bold text-gray-700 mb-2">3D Concept: ${description}</h3>
                    <p class="text-gray-600">This area would display an interactive 3D model in a production environment.</p>
                    <div class="mt-4 p-3 bg-green-50 rounded-lg border border-green-200">
                        <p class="text-green-700 text-sm"><i class="fas fa-info-circle mr-2"></i>Vichaar's AI has generated this visualization based on your input.</p>
                    </div>
                `;
                
                modelPlaceholder.classList.remove('hidden');
                modelCanvas.classList.add('hidden');
            }
            
            function clearChat() {
                // Keep only the welcome message
                const welcomeMessage = document.getElementById('welcomeMessage');
                chatContainer.innerHTML = '';
                chatContainer.appendChild(welcomeMessage);
            }
            
            // Voice input simulation
            voiceButton.addEventListener('click', function() {
                if (voiceButton.classList.contains('bg-white')) {
                    // Start voice input
                    voiceButton.className = 'bg-indigo-600 text-white p-2 rounded-full hover:bg-indigo-700 transition';
                    voiceButton.innerHTML = '<i class="fas fa-microphone-slash"></i>';
                    
                    // Simulate voice input after delay
                    setTimeout(() => {
                        const sampleVoiceInputs = [
                            "I have experience in agriculture and want to start my own business",
                            "I'm a computer science graduate looking for startup ideas",
                            "I'm good at cooking and want to open a food business"
                        ];
                        
                        const randomInput = sampleVoiceInputs[Math.floor(Math.random() * sampleVoiceInputs.length)];
                        userInput.value = randomInput;
                        
                        // Stop voice input
                        voiceButton.className = 'bg-white text-indigo-600 p-2 rounded-full border border-indigo-600 hover:bg-indigo-50 transition';
                        voiceButton.innerHTML = '<i class="fas fa-microphone"></i>';
                    }, 2000);
                } else {
                    // Stop voice input
                    voiceButton.className = 'bg-white text-indigo-600 p-2 rounded-full border border-indigo-600 hover:bg-indigo-50 transition';
                    voiceButton.innerHTML = '<i class="fas fa-microphone"></i>';
                }
            });
            
            // Model viewer controls
            document.getElementById('rotateModel').addEventListener('click', function() {
                alert('In a production environment, this would rotate the 3D model.');
            });
            
            document.getElementById('downloadModel').addEventListener('click', function() {
                alert('3D model download would be available in the full version.');
            });
        });
    </script>
</body>
</html>
