<template>
<div id="preloader">
</div>
<div style="text-align: center; margin-top: 100px;">
<img src="../components/UtyaB.gif" width="250px"><br>
<h3 class="heeloinf">Create ankets of your<br>acquaintances and friends<br>and hate them with us</h3>
<RouterLink to="/home">
    <button class="hatebtn">Go To Hate</button>
</RouterLink>
</div>
</template>

<style scoped>
body {
    touch-action: none;
    overflow: hidden;
}
</style>

<script>
window.addEventListener('load', function() {
    // Убираем стандартное поведение при загрузке, т.к. будем использовать setTimeout
});

// Устанавливаем таймер на 10 секунд (10000 миллисекунд)
setTimeout(function() {
    const preloader = document.getElementById('preloader');
    if (preloader) { // Проверяем, существует ли элемент
        preloader.classList.add('hidden'); // Добавляем класс для скрытия
    }
}, 5000); // 10000 миллисекунд = 10 секунд
</script>
