<template>
<h1 class="active">Stenka</h1>
<RouterLink to="add">
<button class="add">Add Hate</button>
</RouterLink>
<div class="scroolbar" style="overflow-x: scroll; display: flex;">
<RouterLink to="home">
    <button class="hate">Hate</button>
</RouterLink>
<RouterLink to="stenka">
    <button class="stenka">Stenka</button>
</RouterLink>
<RouterLink to="nft">
    <button class="nft">NFT</button>
</RouterLink>
<RouterLink to="task">
    <button class="task">Task</button>
</RouterLink>
</div>
    <div id="post-container" style="overflow-y: scroll;">
      <div v-for="post in posts" :key="post.key" class="post-item" style="margin-top: 12px; max-width: 500px;">
        <b>{{ post.nick }}</b><br>{{ post.text }}
      </div>
    </div>
</template>
  
<script setup>
import { ref, onMounted, onUnmounted } from 'vue';
import { initializeApp } from "firebase/app";
import { getDatabase, ref as dbRef, onValue } from "firebase/database";
  
const firebaseConfig = {
  apiKey: import.meta.env.VITE_FIREBASE_API_KEY,
  authDomain: import.meta.env.VITE_FIREBASE_AUTH_DOMAIN,
  projectId: import.meta.env.VITE_FIREBASE_PROJECT_ID,
  storageBucket: import.meta.env.VITE_FIREBASE_STORAGE_BUCKET,
  messagingSenderId: import.meta.env.VITE_FIREBASE_MESSAGING_SENDER_ID,
  appId: import.meta.env.VITE_FIREBASE_APP_ID,
  measurementId: import.meta.env.VITE_FIREBASE_MEASUREMENT_ID
};
  
  const app = initializeApp(firebaseConfig);
  const db = getDatabase(app);
  const posts = ref([]); 
  
  const postsRef = dbRef(db, 'posts');
  
  onMounted(() => {
  
    const unsubscribe = onValue(postsRef, (snapshot) => { 
      posts.value = []; 
      snapshot.forEach(childSnapshot => {
        posts.value.push({
            key: childSnapshot.key, 
            ...childSnapshot.val()
        });
      });
  });
  onUnmounted(unsubscribe);
}); 
</script>
  
<style scoped>
body {
  touch-action: none;
  overflow-y: scroll;
  -ms-touch-action: none; 
  user-select: none;
  scrollbar-width: none; 
}

.active {
    font-family: Geologica;
    color: white;
}

.post-item {
    background-color: #272727;
    border: 0.5px solid #373737;
    border-radius: 15px;
    color: white;
    font-family: Geologica;
    padding: 10px;
    margin-bottom: 10px;
}

.stenka {
    background-color: rgb(20, 128, 223);
    border: 0.5px solid rgb(15, 120, 212);
    width: 100px;
    height: 30px;
    border-radius: 10px;
    font-family: Geologica;
    color: white;
    margin-left: 10px;
}

.hate {
    background-color: #333333;
    border: 0.5px solid #515151;
    width: 100px;
    height: 30px;
    border-radius: 10px;
    font-family: Geologica;
    color: white;
}

.nft {
    background-color: #333333;
    border: 0.5px solid #515151;
    width: 100px;
    height: 30px;
    border-radius: 10px;
    font-family: Geologica;
    color: white;
    margin-left: 10px;
}

.task {
    background-color: #333333;
    border: 0.5px solid #515151;
    width: 100px;
    height: 30px;
    border-radius: 10px;
    font-family: Geologica;
    color: white;
    margin-left: 10px;
}

.add {
    background-color: rgb(20, 128, 223);
    border: 0.5px solid rgb(15, 120, 212);
    width: 100px;
    height: 30px;
    border-radius: 15px;
    font-family: Geologica;
    color: white;
    float: right;
    margin-top: -50px;
}
</style>
