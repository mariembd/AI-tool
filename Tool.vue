<template>
    <div class="app">
        <aside class="sidebar">
            <div class="nav-item" v-for="item in navItems" :key="item">
                {{ item }} 
           </div>
        </aside>
         <main class="content">
           <h1>AI Tool</h1>
   <div class="ai-tool"> 
           <!-- AI functionality -->
             <textarea v-model="userInput" placeholder="Type your question..." rows="4" >
             </textarea> <button @click="processInput">
               Ask AI
             </button>
       <div v-if="aiResponse">
            <h3>Response:</h3> 
            <p>{{ aiResponse }}</p>
       </div> 
   </div> 
        </main> 
       </div> 
           </template>
            <script>
             export default { data() { return { navItems: ["Start Page", "Notification"], userInput: "", aiResponse: "", }; }, methods: { processInput() { // Replace with the AI tool API logic 
               if (this.userInput) { 
               this.aiResponse = `You asked: "${this.userInput}". AI says: Hello!`; 
                                 }
                else { 
                   this.aiResponse = "Please enter a question."; 
                     } 
                   }, 
               }, 
           }; 
            </script> 
   <style scoped>
       .app { 
           display: flex;     
           height: 100vh; 
           }
       .sidebar {
            width: 200px;
            background-color: #2c3e50;
            color: white;
            padding: 20px; 
            display: flex; 
            flex-direction: column; 
           } 
       .nav-item { 
           margin-bottom: 20px;
           cursor: pointer; 
                } 
       .nav-item:hover {
            text-decoration: underline; 
       } 
       .content {
           flex-grow: 1;
           padding: 20px; 
           } 
       .ai-tool textarea {
            width: 100%; 
            margin-bottom: 10px; 
            } 
       .ai-tool button { 
           padding: 10px 20px;
           background-color: #3498db; 
           color: white; border: none;
           cursor: pointer; 
           } 
       .ai-tool button:hover { 
           background-color: #2980b9;
            }
       .ai-tool h3 { 
           margin-top: 20px;
        } 
   </style>
import axios from "axios"; methods: { async processInput() { if (!this.userInput) { this.aiResponse = "Please enter a question."; return; } try { const response = await axios.post( "https://api.openai.com/v1/completions", { model: "text-davinci-003", // Replace with your model prompt: this.userInput, max_tokens: 100, }, { headers: { Authorization: `Bearer YOUR_API_KEY`, }, } ); this.aiResponse = response.data.choices[0].text.trim(); } catch (error) { console.error(error); this.aiResponse = "An error occurred while communicating with the AI."; } }, },