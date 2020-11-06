<template>
  <div id="container_dad">
        <div class="containerUndef">
            <div class="containerFilme" v-bind:style="{'background-image': 'url(https://image.tmdb.org/t/p/w500'+filme.poster_path+')',}">
                
            </div>
        </div>
        <p>{{filme.original_title}}</p>
  </div>
</template>

<script>
export default {
    name: 'Filmes',
    props:{
        filme:{},
    },
    mounted: function () {
        this.$nextTick(function () {
            if(this.filme.poster_path ==  null){
                console.log('bg filme null');
            }
        })
    }
};



</script>

<style>

.containerFilme{
    width: 280px;
    height: 400px;
    background-image: url("./../assets/no_image.png");
    background-position: center;
    background-size: cover;
    box-shadow: 0 3px 6px rgba(0,0,0,0.16), 0 3px 6px rgba(0,0,0,0.23);
    cursor: pointer;
}
.containerUndef{
    width: 280px;
    height: 400px;
    background-color: white;
    background-image: url("./../assets/no_image.png");
    background-position: center;
    background-size: cover;
}
#container_dad p{
    color: white;
    width: 280px;
    text-align: center;
    margin-bottom: 100px;
}

</style>