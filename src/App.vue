<template>
  <div id="app">
    <div id="modal" v-on:click="closeModal()">
      <div class="modal_container">
        <div class="img_modal">
          <img id="path" src="" alt="">
        </div>
        <div class="other_infos">
          <h1 id="title"></h1>
          
          <label for="">Gênero</label>
          <p id="genres"></p>
          <br>

          <label for="">PT/BR</label>
          <p id="overview_br"></p>

          <br>

          <label for="">ENG</label>
          <p id="overview"></p>

          

          
        </div>
      </div>
    </div>
    <Menu/>
    <div id="container_list">
      <div v-for="(filme, index) in filmes"  :key="index" v-on:click="infoFilme(filme)">
        <Filmes :filme="filme" />
      </div>
    </div>
    <div class="btn_see_more">
      <button>Ver mais</button>
    </div>
    <Footer/>
  </div>
</template>

<script>
import Filmes from "./components/Filmes";
import Footer from "./components/Footer";
import Menu from "./components/Menu";
import axios from "axios";

export default {
  name: 'App',
  data(){
    return{
      filmes: []
    }
  },
  components: {
    Filmes,
    Footer,
    Menu,
  },

  methods:{
    infoFilme(filme){
      document.getElementById('title').innerHTML = filme.original_title;
      document.getElementById('genres').innerHTML = filme.genres[0].name;
      document.getElementById('overview').innerHTML = filme.overview;
      document.getElementById('overview_br').innerHTML = filme.overview;
      document.getElementById('path').src = "https://image.tmdb.org/t/p/w500"+filme.poster_path;
      document.getElementById('modal').style.display = "flex";
    },
    closeModal(){
      document.getElementById('modal').style.display = "none";
    }
  },
  created: function(){
    for (let i = 0; i < 80 ; i++) {
      axios.get("https://api.themoviedb.org/3/movie/"+i+"?api_key=db9c7903a0212a28fa44032cf50d7771").then((resp)=>{
        this.filmes.push(resp.data);
      })
    }
  }

}


</script>

<style>

/* ALl Style */

#app{
  flex-direction: column;
  display: flex;
  background-color: #363636b9;
  background-image: url('../src/assets/marvelbg.png');
}
#container_list{
  padding-top: 80px;
  width: 78vw;
  margin: 0 auto;
  justify-content: space-between;
  flex-wrap:wrap;
  display: flex;
}
.btn_see_more{
  justify-content: center;
  display: flex;
  padding-bottom: 80px;
  width: 100%;
}
.btn_see_more button{
  padding: 12px;
  width: 300px;
  cursor: pointer;
}

/* Modal */
#modal{
  width: 100%;
  height: 100%;
  justify-content: center;
  align-items: center;
  position: fixed;
  display: none;
  background-color: rgba(0, 0, 0, 0.5);
}
.modal_container{
  width: 50%;
  height: 600px;
  border-radius: 5px;
  overflow: hidden;
  box-shadow: 0 3px 6px rgba(0,0,0,0.16), 0 3px 6px rgba(0,0,0,0.23);
  background-color: white;
  display: flex;
}
.img_modal{
  min-width: 30%;
  justify-content: center;
  display: flex;
  overflow: hidden;
}
.img_modal img{
  height: 100%;
}
.other_infos{
  flex-direction: column;
  display: flex;
  width: auto;
}
.other_infos h1{
  background-color: black;
  color: white;
  margin: 0px;
  margin-bottom: 4%;
  padding: 25px;
}
.other_infos p{
  font-size: 18px;
  margin: 0px;
  padding: 5px 25px;
}
.other_infos label{
  padding: 10px 25px;
  font-weight: bold;
}

/* Responsivity */
@media screen and (max-width: 680px) {
   #container_list{
     justify-content: center;
   }
}

</style>
