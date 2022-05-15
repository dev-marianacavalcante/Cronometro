<template>
  <div id="app">
    <div class="time">
      <button class="button" @click="startCron()">Iniciar</button>
      <button class="button" @click="stopCron()">Parar</button>
      <button class="button" @click="restartCron()">Reiniciar</button>
    </div>
    <div class="container">
      <p class="text font-text">{{formattime}}</p>
    </div>
    <footer class="footer">
      <p>Feito com ❤️ por <a target="_blank" href="https://github.com/maricavalcante">Mariana Cavalcante</a></p>
    </footer>
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      seconds: 0,
      minutes: 0,
      hours: 0,
      intervalid: ''
    }
  },
  methods: {
    startCron() {
      if (this.intervalid) {
        return false
      }
      this.intervalid = setInterval(() => {
        this.updateTime();
      }, 1000)
    },
    updateTime() {
      this.seconds++
      if (this.seconds == 60) {
        this.seconds = 0
        this.minutes++
      }
      if (this.minutes == 60) {
        this.minutes = 0
        this.hours++
      }
    },
    stopCron() {
      clearInterval(this.intervalid)
      this.intervalid = ''
    },
    restartCron(){
      this.stopCron();
      this.seconds = 0
      this.minutes = 0
      this.hours = 0
    }
  },
  computed: {
    formattime(){
      
      return `${this.hours < 10 ? `0${this.hours}` : this.hours}:${this.minutes < 10 ? `0${this.minutes}` : this.minutes}:${this.seconds < 10 ? `0${this.seconds}` : this.seconds}`
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,400;1,600&display=swap');
html, body {
  height: 100vh;
  margin: 0;
  background-image: url("./assets/background.avif");
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;
}
a{
  color: white;
  font-size: 16px;
  font-family: 'Montserrat', sans-serif;
}
a:link {
  text-decoration: none;
  }
a:visited {
  text-decoration: none;
}

a:hover {
  text-decoration: underline;
}
a:active {
  text-decoration: underline;}

#app{
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}
.time{
  display: flex;
  align-items: center;
  height: 30vh;
  justify-content: center;
}
.container{
  display: flex;
  align-items: center;
  justify-content: center;
  background:rgba(0, 0, 0, 0.26);
  width: 488px;
  height: 244px;
  border: none ;
  border-radius: 10px;
  backdrop-filter: blur( 3px );
  -webkit-backdrop-filter: blur( 8px );
}
.text{
  font-size: 5em;
}
.font-text {
  font-family: 'Montserrat', sans-serif;
  color: #ffffff;
}
.button{
  text-decoration: underline;
  background-color: transparent;
  padding: 10px 24px;
  font-size: 24px;
  border: 0 none;
  cursor: pointer;
  color: #ffffff;
}
.footer {
  color: white;
  font-size: 16px;
  font-family: 'Montserrat', sans-serif;
}
</style>