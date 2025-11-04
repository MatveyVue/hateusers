<template>
  <div style="text-align: center; font-family: Geologica; color: white; margin-top: 20px;">
  <h1>Create Message<br>To Stenka</h1>
  </div>
  <div style="text-align: center; margin-top: 50px;">
      <input id="nick" class="nick" type="text" v-model="newPost.nick" readonly><br>
      <textarea class="mess" v-model="newPost.text" placeholder="Your Message"></textarea><br>
  <RouterLink to="stenka">
      <button class="send" @click="submitPost">Send</button>
  </RouterLink>
  </div>
  </template>
    
  <script setup>
  import { ref, onMounted, reactive } from 'vue';
  import { initializeApp } from 'firebase/app';
  import { getDatabase, ref as dbRef, push, onValue } from 'firebase/database';
    
  const firebaseConfig = {
    apiKey: import.meta.env.VITE_FIREBASE_API_KEY,
    authDomain: import.meta.env.VITE_FIREBASE_AUTH_DOMAIN,
    projectId: import.meta.env.VITE_FIREBASE_PROJECT_ID,
    storageBucket: import.meta.env.VITE_FIREBASE_STORAGE_BUCKET,
    messagingSenderId: import.meta.env.VITE_FIREBASE_MESSAGING_SENDER_ID,
    appId: import.meta.env.VITE_FIREBASE_APP_ID,
    measurementId: import.meta.env.VITE_FIREBASE_MEASUREMENT_ID
  };
    
  const newPost = reactive({
      nick: window.Telegram.WebApp.initDataUnsafe.user ? window.Telegram.WebApp.initDataUnsafe.user.username : null,
      text: ''
  });
    
  const posts = ref([]);
    
    const submitPost = () => {
      if (newPost.nick && newPost.text) {
        const app = initializeApp(firebaseConfig);
        const db = getDatabase(app);
        const postsRef = dbRef(db, 'posts');
        push(postsRef, newPost)
          .then(() => {
            console.log("Data written successfully!");
            newPost.nick = window.Telegram.WebApp.initDataUnsafe.user ? window.Telegram.WebApp.initDataUnsafe.user.username : null;
            newPost.text = '';
          })
          .catch((error) => {
            console.error("Error writing data:", error);
            alert("There was an error posting your message."); // User-friendly alert
          });
      } else {
        alert("Please fill in both nickname and message fields.");
      }
    };
    
    
    onMounted(() => {
      const app = initializeApp(firebaseConfig);
      const db = getDatabase(app);
      const postsRef = dbRef(db, 'posts');
    
      onValue(postsRef, (snapshot) => {
        posts.value = [];
        snapshot.forEach(childSnapshot => {
            posts.value.push({
              key: childSnapshot.key,
              ...childSnapshot.val()
            });
          });
      });
    
  });
  </script>
    
  <style scoped>
  body {
      touch-action: none;
  }
  
  #post-container {
      margin-top: 20px;
  }
  
  .post-item {
      border: 1px solid #ccc;
      padding: 10px;
      margin-bottom: 10px;
  }
  
  .nick {
      background-color: #272727;
      border: 0.5px solid #373737;
      height: 40px;
      width: 95%;
      border-radius: 15px;
      font-family: Geologica;
      color: white;
      max-width: 500px;
      font-size: 16px;
  }
  
  .mess {
      background-color: #272727;
      border: 0.5px solid #373737;
      height: 120px;
      width: 95%;
      border-radius: 15px;
      margin-top: 10px;
      font-family: Geologica;
      color: white;
      max-width: 500px;
      font-size: 16px;
  }
  
  .send {
      background-color: rgb(19, 127, 222);
      font-family: Geologica;
      font-size: 16px;
      color: white;
      border: none;
      width: 95%;
      height: 45px;
      border-radius: 10px;
      max-width: 500px;
      margin-top: 10px;
  }
  </style>
  
