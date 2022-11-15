<template>

<div class="center"> 
    <div class="card card-custom">
        <div @click="mudarSprite" class="card-image">
            <figure class="image" :class="pokemon.class">
            <img :src="currentImg" alt="Placeholder image">
            </figure>
        </div>
        <div class="card-content is-justify-content-center">
            <div class="media">
            <div class="media-content">
                <span class="has-text-weight-bold">{{upper}}</span><br>
                <span>Type: {{pokemon.type}}</span>
            </div>
            </div>

            <div class="content">
            </div>
        </div>
</div>
</div>
</template>

<script>
import axios from 'axios'

export default {
    name: "Pokemon",
    data() {
        return {
            isFront: true,
            currentImg: '',
            pokemon: {
                type: '',
                front: '',
                back: '',
                class: ''
            },
        }
    },
    created: function() {
        axios.get(this.url).then(res => {
            this.pokemon.type = res.data.types[0].type.name

            this.pokemon.front = res.data.sprites.front_default;

            this.pokemon.back = res.data.sprites.back_default;

            this.pokemon.class = `border-${this.pokemon.type}`
            
            this.currentImg = this.pokemon.front
        }).catch(err => {
            console.log(err)
        });
    },
    props:{
        name:String,
        url: String,
        num: Number
    },
    computed:{
        upper(){
            let newName = this.name[0].toUpperCase() + this.name.slice(1)
            return newName
        }
    },
    methods:{
        mudarSprite: function() {
            if(this.isFront){
                this.isFront =  false
                this.currentImg = this.pokemon.back
            } else {
                this.isFront =  true
                this.currentImg = this.pokemon.front
            }
        }
    }
}
</script>

<style scoped>
.center {
    display: flex;
    flex-direction: column;
    align-items: center;
}
.card-custom {
    width: 200px;
    margin: 12px;
}
.border-fire {
    border-left: 3px solid rgb(214, 0, 0);
}
.border-electric {
    border-left: 3px solid rgb(248, 232, 0);
}
.border-poison {
    border-left: 3px solid rgb(133, 0, 167);
}
.border-normal {
    border-left: 3px solid rgb(124, 124, 124);
}
.border-water {
    border-left: 3px solid rgb(0, 150, 219);
}
.border-bug {
    border-left: 3px solid rgb(0, 179, 0);
}
.border-ground {
    border-left: 3px solid rgb(153, 107, 7);
}
.border-fairy {
    border-left: 3px solid rgb(255, 2, 255);
}
.border-fighting {
    border-left: 3px solid rgb(102, 15, 15);
}
.border-psychic {
    border-left: 3px solid rgb(102, 15, 15);
}
.border-rock {
    border-left: 3px solid rgb(177, 94, 0);
}
.border-ghost {
    border-left: 3px solid rgb(70, 19, 71);
}
.border-ice {
    border-left: 3px solid rgb(0, 217, 255);
}
.border-dragon {
    border-left: 3px solid rgb(255, 64, 64);
}
.border-grass {
    border-left: 3px solid rgb(28, 241, 0);
}
.image {
    cursor: pointer;
}
</style>
