<template>
<div id="preloader">
</div>
<h1 class="active">Hate</h1>
<a href="https://t.me/haterusers">
<button class="add">Add Hate</button>
</a>
<div class="scrollbar" style="overflow-x: scroll; display: flex;">
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
<div v-for="(person, index) in profile" :key="index" class="ankets">
      <img class="icon" :src="person.icon" alt="Profile Icon" v-if="person.icon">
      <p class="nick">{{ person.nick }}</p>
      <p class="infd">{{ person.infd }}</p>
      <p class="info">{{ person.info }}</p>
<ul class="tags" v-if="person.tags">
    <li v-for="tag in person.tags" :key="tag">{{ tag }}</li>
</ul>
</div> 
</template>
  
<script setup>
import { profile, open } from '../script/home.js'; 
console.log(profile.value); 

window.addEventListener('load', function() {
    // Убираем стандартное поведение при загрузке, т.к. будем использовать setTimeout
});

// Устанавливаем таймер на 10 секунд (10000 миллисекунд)
setTimeout(function() {
    const preloader = document.getElementById('preloader');
    if (preloader) { // Проверяем, существует ли элемент
        preloader.classList.add('hidden'); // Добавляем класс для скрытия
    }
}, 3000); // 10000 миллисекунд = 10 секунд
</script>
  
<style scoped>
body {
    touch-action: none;
    overflow-y: scroll;
}

.active {
    font-family: Geologica;
    color: white;
}

.ankets {
    background-color: #272727;
    border-radius: 15px;
    padding: 3px;
    margin-bottom: 10px;
    max-width: 450px;
    margin-top: 15px;
    border: 0.5px solid #343434;
}

.tags {
    list-style: none;
    padding: 0;
    margin: 0;
    display: flex; 
    flex-wrap: wrap;
    font-family: Geologica;
    color: white;
    margin-left: 12px;
    margin-top: 15px;
}

.tags li {
    background-color: #303030;
    padding: 5px 10px; 
    margin-right: 5px;
    border-radius: 8px;
    margin-bottom: 5px;
}

.nick {
    font-family: Geologica;
    color: rgb(27, 130, 221);
    font-size: 18px;
    margin-top: 12px;
    margin-left: 55px;
}

.info {
    font-family: Geologica;
    color: white;
    font-size: 16px;
    margin-left: 15px;
}

.icon {
    width: 40px;
    float: left;
    margin-left: 10px;
    margin-top: 10px;
}

.infd {
    font-family: Geologica;
    color: rgb(109, 109, 109);
    font-size: 14px;
    margin-top: -18px;
    margin-left: 57px;
}

.ankets:active {
  border: 0.3px solid rgb(20, 128, 223);
  transform: translateY(-5px);
  background-color: rgb(44, 44, 44);
}

.ankets:hover {
  border: 0.5px solid rgb(20, 128, 223);
  transform: translateY(-5px);
  background-color: rgb(44, 44, 44);
}

.modal {
    background-color: #292929;
    width: 100%;
    height: 80%;
    position: absolute;
    bottom: 0;
    margin-left: -8px;
    border-top-left-radius: 25px;
    border-top-right-radius: 25px;
}

.stenka {
    background-color: #333333;
    border: 0.5px solid #515151;
    width: 100px;
    height: 30px;
    border-radius: 10px;
    font-family: Geologica;
    color: white;
    margin-left: 10px;
}

.hate {
    background-color: rgb(20, 128, 223);
    border: 0.5px solid rgb(15, 120, 212);
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
