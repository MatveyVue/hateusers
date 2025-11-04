<template>
<div style="text-align: center; font-family: Geologica; color: white; margin-top: 20px;">
<h1>Create Message<br>To Stenka</h1>
</div>
<div style="text-align: center; margin-top: 50px;">
    <input id="nickname" class="nick" type="text" :readonly="!!telegramUsername" :disabled="!isTelegramReady" v-model="newPost.nick" placeholder="Your Nickname"><br>
    <textarea class="mess" v-model="newPost.text" placeholder="Your Message"></textarea><br>
<RouterLink to="stenka">
    <button class="send" @click="submitPost">Send</button>
</RouterLink>
</div>
</template>
  
<script setup>
import { ref, onMounted, reactive } from 'vue';
// Если вы используете Vue Router, импортируйте RouterLink
import { RouterLink } from 'vue-router'; // Убедитесь, что Vue Router установлен и настроен

import { initializeApp } from "firebase/app";
import { getDatabase, ref as dbRef, push, onValue } from "firebase/database";
import TelegramSDK from '@telegram-apps/sdk';

// --- Firebase Configuration ---
// !!! ВАЖНО: Замените import.meta.env.VITE_... на ваши реальные значения, если не используете .env файл !!!
const firebaseConfig = {
  apiKey: import.meta.env.VITE_FIREBASE_API_KEY || "API_KEY_HERE", // Замените "API_KEY_HERE" если VITE переменные не работают
  authDomain: import.meta.env.VITE_FIREBASE_AUTH_DOMAIN || "merry-wish.firebaseapp.com",
  projectId: import.meta.env.VITE_FIREBASE_PROJECT_ID || "merry-wish",
  storageBucket: import.meta.env.VITE_FIREBASE_STORAGE_BUCKET || "merry-wish.firebasestorage.app",
  messagingSenderId: import.meta.env.VITE_FIREBASE_MESSAGING_SENDER_ID || "472160350126",
  appId: import.meta.env.VITE_FIREBASE_APP_ID || "1:472160350126:web:13ccce689eccd0106be23f",
  measurementId: import.meta.env.VITE_FIREBASE_MEASUREMENT_ID || "G-2FV9T3RFY0",
  databaseURL: import.meta.env.VITE_FIREBASE_DATABASE_URL || "https://merry-wish-default-rtdb.firebaseio.com"
};

// --- Инициализация Firebase (один раз) ---
const app = initializeApp(firebaseConfig);
const db = getDatabase(app);
const postsRef = dbRef(db, 'posts');

// --- Состояние компонента ---
const newPost = reactive({
    nick: '', // Будет заполняться Telegram username или введен вручную
    text: ''  // Поле для ввода сообщения
});
const posts = ref([]); // Для отображения постов из Firebase
const telegram = new TelegramSDK(); // Инициализация Telegram SDK
const isTelegramReady = ref(false); // Флаг готовности Telegram SDK
const telegramUsername = ref(''); // Отдельно храним username для удобства
const isLoadingPosts = ref(false); // Флаг загрузки постов
const isSubmittingPost = ref(false); // Флаг отправки поста

// --- Функции ---

const submitPost = async () => {
    // Проверка полей
    if (!newPost.nick || !newPost.text) {
      alert("Please fill in both nickname and message fields.");
      return;
    }

    // Проверяем, что Telegram SDK готов и есть username
    if (!isTelegramReady.value || !newPost.nick) {
        alert("Please wait for Telegram to load or ensure you have a username.");
        return;
    }

    isSubmittingPost.value = true; // Начинаем отправку
    try {
        // Используем push для автоматической генерации ключа, что предпочтительнее для списков
        await push(postsRef, { nick: newPost.nick, text: newPost.text }); // Отправляем объект с nick и text
        console.log("Data written successfully!");

        // Очищаем только поле текста, так как nick должен оставаться Telegram username (или введенный вручную)
        newPost.text = '';
        alert("Your message has been posted!");
    } catch (error) {
        console.error("Error writing data:", error);
        alert("There was an error posting your message.");
    } finally {
        isSubmittingPost.value = false; // Завершаем отправку
    }
};

onMounted(async () => {
    try {
        await telegram.ready(); // Убедимся, что Telegram SDK готов
        isTelegramReady.value = true;

        if (telegram.initDataUnsafe.user && telegram.initDataUnsafe.user.username) {
            newPost.nick = telegram.initDataUnsafe.user.username; // Автоматически заполняем nick
            telegramUsername.value = telegram.initDataUnsafe.user.username; // Сохраняем для readonly
            console.log('Telegram username automatically set:', newPost.nick);
        } else {
            console.log('Telegram user has no username or not running in Telegram Web App.');
            // Если username нет, поле nick останется пустым. Пользователь должен будет ввести его сам.
            // alert("Could not retrieve your Telegram username. Please enter it manually."); // Можно показать alert, если нужно
        }
    } catch (error) {
        console.error('Error initializing Telegram SDK:', error);
        alert('Failed to initialize Telegram Web App. Please try again.');
        isTelegramReady.value = false; // Указываем, что Telegram SDK не готов
    }

    // --- Подписка на обновления Firebase ---
    isLoadingPosts.value = true; // Начинаем загрузку
    onValue(postsRef, (snapshot) => {
        posts.value = []; // Очищаем перед обновлением
        snapshot.forEach(childSnapshot => {
            posts.value.push({
                id: childSnapshot.key, // Используем id для ключа в v-for
                ...childSnapshot.val()
            });
        });
        isLoadingPosts.value = false; // Загрузка завершена
    }, (error) => {
        console.error("Error fetching posts:", error);
        isLoadingPosts.value = false;
        alert("Failed to load messages.");
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
