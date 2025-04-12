<template>
    <h1 class="active">Task</h1>
<div class="scrollbar" style="overflow-x: scroll; display: flex;">
<RouterLink to="home">
    <button @click="anotherAction" class="hate">Hate</button>
</RouterLink>
<RouterLink to="stenka">
    <button @click="anotherAction" class="stenka">Stenka</button>
</RouterLink>
<RouterLink to="nft">
    <button @click="anotherAction" class="nft">NFT</button>
</RouterLink>
<RouterLink to="task">
    <button @click="anotherAction" class="task">Task</button>
</RouterLink>
</div>

<div class="story">
    <img class="imgstory" src="../components/hatewhsxg.jpg" width="160px">
    <p style="margin-left: 5px; margin-top: 165px; position: absolute; font-family: Geologica; color: white;">Hate Story</p>
    <p style="font-family: Geologica; font-size: 12px; color: grey; margin-left: 5px; margin-top: 185px; position: absolute;">Tyler's first assignment...</p>
    <button @click="shareToStory()" class="share">Share To Story</button>
</div>
</template>

<script>
export default {
  data() {
    return {
      storyImage: 'https://i.postimg.cc/GmmhB85X/hatewhsxg.jpg',
      storyText: '@HateUsersBot and go hate your friends, also don\'t forget to visit the channel @hatewhsxg'
    };
  },
  methods: {
    shareToStory() {
      if (typeof Telegram.WebApp !== 'undefined') {
        Telegram.WebApp.shareToStory(this.storyImage, { text: this.storyText })
          .then(result => {
            console.log('Story shared successfully:', result);
          })
          .catch(error => {
            console.error('Error sharing to story:', error);
            alert("Ошибка при публикации истории: " + error.message);
          });
      } else {
        console.error("Telegram.WebApp не доступен");
        alert("Эта функция доступна только в Telegram Web App");
      }
    },
    anotherAction() {
      console.log("Другая кнопка нажата");
    }
  }
};

</script>

<style scoped>
body {
    touch-action: none;
}
    
.active {
    font-family: Geologica;
    color: white;
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
    background-color: rgb(20, 128, 223);
    border: 0.5px solid rgb(15, 120, 212);
    width: 100px;
    height: 30px;
    border-radius: 10px;
    font-family: Geologica;
    color: white;
    margin-left: 10px;
}

.imgstory {
    margin-top: 15px;
    border-top-left-radius: 15px;
    border-top-right-radius: 15px;
    position: absolute;
    margin-top: 3px;
}

.story {
    background-color: #272727;
    width: 160px;
    height: 240px;
    border-radius: 15px;
    margin-top: 15px;
}

.share {
    background-color: rgb(21, 120, 207);
    font-family: Geologica;
    color: white;
    border: none;
    width: 160px;
    height: 35px;
    border-bottom-right-radius: 15px;
    border-bottom-left-radius: 15px;
    margin-top: 210px;
}
</style>
