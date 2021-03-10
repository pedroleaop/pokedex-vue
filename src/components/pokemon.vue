<template>
  <div id="pokemon">
  <h1></h1>

        <div class="card">
        <div class="card-image">
            <figure class="image is-4by3">
            <img :src="currentImg" @mouseup="mudarVisao" alt="Placeholder image">
            </figure>
            
        </div>
        <div class="card-content">
            <div class="media">
            <div class="media-left">
                <figure class="image is-48x48">                </figure>
            </div>
            <div class="media-content">
                <p class="title is-4">{{num}} - {{name | upper}}</p>
                <p class="subtitle is-6">{{pokemon.type}}</p>
            </div>
            </div>
            <div class="content">
                <button class="button is-medium is-fullwidth" @click="mudarVisao">Mudar visão</button>
            </div>
        </div>
        </div>

  </div>
</template>

<script>
import axios from 'axios';
export default {
    data(){
        return{
            isFront: true,
            currentImg: '',
            pokemon: {
                type: '',
                front: '',
                back: ''
            }
        }
    },
    created: function(){
        axios.get(this.url).then(res => {
            this.pokemon.type = res.data.types[0].type.name;
            this.pokemon.front = res.data.sprites.front_default;
            this.pokemon.back = res.data.sprites.back_default;
            this.currentImg = this.pokemon.front;
            console.log(this.pokemon);
        })
    },
    props: {
        num: Number,
        name: String,
        url: String
    },
    filters: {
        upper: function(value) {
            var NewName = value[0].toUpperCase() + value.slice(1);
            return NewName;
        }
    },
    methods: {
        mudarVisao: function(){
            if(this.isFront){
                this.isFront = false;
                this.currentImg = this.pokemon.back;
            }
            else {
                this.isFront = true;
                this.currentImg = this.pokemon.front;
            }
            }
    }
}
</script>

<style>

img {
    background-color: rgb(223, 223, 223);
    image-rendering: -moz-crisp-edges;
image-rendering: -webkit-crisp-edges;
image-rendering: pixelated;
image-rendering: crisp-edges;
}

#pokemon {
    margin-top: 2%;
}

</style>