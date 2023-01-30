<script setup>
  import {ref} from "vue";

  const showModal = ref(false)
  const newNews = ref("")
  const errorMessage = ref("")
  const newses = ref([])

  function getRandomColor() {
    return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
    
  }

  const addNews = () => {
    if(newNews.value.length < 5) {
      return errorMessage.value = "Cooбщение должно содержать более 5 символов!"
    } 

    newses.value.push({
      id: Math.floor(Math.random() * 1000000),
      text: newNews.value,
      date: new Date(),
      backgroundColor: getRandomColor()
    })
    showModal.value = false
    newNews.value = ""
    errorMessage.value = ""

  }

</script>

<template>
  <main>
    <div v-if="showModal" class="overlay">
      <div class="modal">
        <textarea v-model.trim="newNews" name="news" id="news" cols="30" rows="10"> </textarea>
        <p v-if="errorMessage"> {{errorMessage}}</p>
        <button @click="addNews">Add news</button>
        <button class="close" @click="showModal = false">Add news</button>
      </div>
    </div>
 <div class="container">
  <header>
    <h1>News</h1>
    <button @click="showModal = true">+</button>
  </header>

  <div class="cards-container">
    <div 
    v-for="news in newses" 
    :key="news.id"
    class="card" 
    :style="{backgroundColor: news.backgroundColor}"

    >
        <p class="main-text"> {{news.text}} </p>
        <p class="date"> {{news.date.toLocaleDateString("ru")}} </p>
    </div>
  </div>

 </div>

  </main>
</template>

<style scoped>
  main {
    height: 100vh;
    width: 100vw;
  }
  .container {
    max-width: 1000px;
    padding: 10px;
    margin: 0 auto;
  }

  header {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  h1 {
    font-weight: 700;
    margin-bottom: 25px;
    font-size: 55px;
  }

  header button {
    border: none;
    padding: 10px;
    width: 50px;
    height: 50px;
    cursor: pointer;
    background-color: rgb(21,20,20);
    border-radius: 100%;
    color: azure;
    opacity: 0.9;
    font-size: 20px;
  }

  .card {
    width: 250px;
    height: 250px;
    background-color: rgb(237, 182, 44);
    padding: 15px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    margin-right: 20px;
    margin-bottom: 20px;
    border-radius: 15px;  
  }

  .date {
    font-size: 12px;
    font-weight: 700;
  }

  .cards-container {
    display: flex;
    flex-wrap: wrap;
  }

  .overlay {
    position: absolute;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.77);
    z-index: 10;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .modal {
    width: 750px;
    background-color: #fff;
    border-radius: 10px;
    padding: 30px;
    position: relative;
    display: flex;
    flex-direction: column;
  }

  .modal button {
    padding: 10px 20px;
    font-size: 20px;
    width: 100%;
    background-color: blueviolet;
    border: none;
    color: #fff;
    cursor: pointer;
    margin-top: 15px;
  }

  .modal .close {
    background-color: rgb(237, 51, 51);
    margin-top: 7px;
  }

  .modal p {
    color: rgb(237, 51, 51);
  }

</style>