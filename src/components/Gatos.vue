<template>
  <div style="backgroundColor: skyblue;">
      <h1>Random Gif Cat</h1>
      <div>
          <form @submit.prevent="obtenerGatito">
              <div class="formColor">
                    <div>
                        <label>Titulo : </label>
                        <input type="text" v-model="titulo">
                    </div>
                    <div>
                        <label>Filtro : </label>
                        <select v-model="filtro">
                            <option>blur</option>
                            <option>mono</option>
                            <option>sepia</option>
                            <option>negative</option>
                            <option>paint</option>
                        </select>
                    </div>
                    <div>
                        <label>Color : </label>
                        <select v-model="color">
                            <option value="red">rojo</option>
                            <option value="green">verde</option>
                            <option value="blue">azul</option>
                            <option value="purple">morado</option>
                            <option value="orange">naranja</option>
                            <option value="yellow">amarillo</option>
                        </select><span class="ball" :style="{backgroundColor: this.color}"></span>
                    </div>
                    <div>
                        <label>Tamaño : </label>
                        <input type="number" v-model="tamano">
                    </div>
              </div>
            
            <button type="submit">Obtener mi Gatito</button>
        </form>
      </div>
      <div>
          <img v-if="imagen" :src="imagen" alt="gatito">
      </div>
      <small>Powered by <a href="https://cataas.com/" target="_blank">cataas.com</a></small>
  </div>
</template>

<script>
export default {
    name: 'Gatos',
    data() {
        return {
            titulo: 'Miau',
            filtro: 'sepia',
            color: 'red',
            tamano: '300',
            imagen: '',
            load: false,
        }
    },
    methods: {
        obtenerGatito(){
            /* 
                https://media3.giphy.com/media/mFTRCmlZgMEr5CHmOV/giphy.gif 
                + https://ezgif.com/resize + imgur.com
                = https://i.imgur.com/Kd4kIzZ.gif
            */
            this.imagen = 'https://i.imgur.com/Kd4kIzZ.gif'
            if(this.titulo && this.filtro && this.tamano && this.color){
                fetch(`https://cataas.com/cat/gif/says/${this.titulo}?filter=${this.filtro}&size=${this.tamano}&color=${this.color}`)
                .then(res =>{
                    this.imagen = res.url
                })
            }   
        }
    },
    created() {
        this.imagen = 'https://i.imgur.com/Kd4kIzZ.gif'
        if(this.titulo && this.filtro && this.tamano && this.color){
                fetch(`https://cataas.com/cat/gif/says/${this.titulo}?filter=${this.filtro}&size=${this.tamano}&color=${this.color}`)
                .then(res =>{
                    this.imagen = res.url
                })
                .catch(error => console.log(error))
            } 
    },
}
</script>

<style scoped>
    *, body{
        margin: 0;
        padding: 0;
        font-family:'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }
    h1{
        text-align: center;
        line-height: 100px;
    }
    small{
        display: block;
        text-align: center;
    }
    img{
        display: block;
        margin-left: auto;
        margin-right: auto;
        height: 300px;
    }
    .ball{
        display: inline-block;
        height: 20px;
        width: 20px;
        margin-left: 20px;
        border-radius: 100%;
    }
    .formColor{
        background-color: pink;
        text-align: left;
        padding-left: 30vw;
    }
    button{
        display: block;
        margin-left: auto;
        margin-right: auto;
        margin-top: 20px;
        margin-bottom: 20px;
        padding: 10px 15px;
        font-weight: bold;
    }
    select, input{
        margin-top: 10px;
        margin-bottom: 10px;
    }
    img{
        margin-top: 50px;
        margin-bottom: 50px;
    }
    label{
        margin-right: 10px;
    }
</style>