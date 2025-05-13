<template>
<h1 class="active">NFT</h1>
<a href="https://t.me/haterusers">
   <button class="add">Add NFT</button>
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
    
<div class="nftcont">
    <img src="../components/cap.png" width="170px" style="margin-top: -20px; margin-left: -5px;">
        <div class="infonft">
            <p style="margin-left: 5px; margin-top: 5px;">Hate Caps</p>
            <p style="font-size: 12px; color: grey; margin-left: 5px; margin-top: -12px;">Quantity: 10 Caps</p>
    <a href="https://hatepay.vercel.app/">
            <button class="claim">Claim 1 TON</button>
    </a>
</div>
</div>
</template>
    
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
    background-color: rgb(20, 128, 223);
    border: 0.5px solid rgb(15, 120, 212);
    width: 100px;
    height: 30px;
    border-radius: 10px;
    font-family: Geologica;
    color: white;
    margin-left: 10px;
}
    
.nftcont {
    background-color: #2b2b2b;
    width: 160px;
    height: 200px;
    border-radius: 15px;
    margin-top: 15px;
}
    
.infonft {
    background-color: #242424;
    width: 160px;
    height: 70px;
    position: absolute;
    margin-top: -20px;
    font-family: Geologica;
    color: white;
    border-bottom-right-radius: 15px;
    border-bottom-left-radius: 15px;
}
    
.claim {
    background-color: rgb(21, 120, 207);
    font-family: Geologica;
    color: white;
    border: none;
    width: 160px;
    height: 35px;
    border-bottom-right-radius: 15px;
    border-bottom-left-radius: 15px;
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
</style>
