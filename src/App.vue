<template>
  <v-app>
  <div class="
    dragFont
    w-full
    h-screen
    bg-gradient-to-r
    from-gray-200
    via-gray-100
    to-gray-50
    background-animate
    overflow-x-auto overflow-y-auto
  ">
  <nav class="backdrop-blur-sm bg-gray-900/30 border-gray-200 px-2 sm:px-4 py-2.5">
    <div class="container flex flex-wrap justify-between items-center mx-auto">
      <a href="https://www.canva.com/design/DAFP7voRtE8/P2936FjlT0WaPotbt45o-g/view?utm_content=DAFP7voRtE8&utm_campaign=designshare&utm_medium=link2&utm_source=sharebutton" class="flex items-center">
          <span class="self-center text-xl font-semibold whitespace-nowrap dark:text-white">Student Simple Helpdesk Support</span>
      </a>

      <addNewTicket></addNewTicket>
      <button v-if="mode!='board'" @click="switchMode('board')" class="inline-flex bg-gray-600 w-12 h-12 p-2 mr-4 rounded-full hover:bg-yellow-500" v-bind="attrs" v-on="on" >
          <font-awesome-icon class="text-white w-8 h-8" icon="fa-solid fa-chalkboard" />
      </button>
      <div v-if="mode=='board'" class="disabled inline-flex bg-teal-600 w-12 h-12 p-2 mr-4 rounded-full" v-bind="attrs" v-on="on" >
        <font-awesome-icon class="text-white w-8 h-8" icon="fa-solid fa-chalkboard" />
      </div>

      <button v-if="mode!='table'" @click="switchMode('table')" class="inline-flex bg-gray-600 w-12 h-12 p-2 mr-4 rounded-full hover:bg-yellow-500" v-bind="attrs" v-on="on" >
        <font-awesome-icon class="text-white w-8 h-8" icon="fa-solid fa-table-list" />
      </button>
      <div v-if="mode=='table'" class="disabled inline-flex bg-teal-600 w-12 h-12 p-2 mr-4 rounded-full" v-bind="attrs" v-on="on" >
        <font-awesome-icon class="text-white w-8 h-8" icon="fa-solid fa-table-list" />
      </div>

      <!-- <button v-if="mode!='list'" @click="switchMode('list')" class="inline-flex bg-gray-600 w-12 h-12 p-2 mr-4 rounded-full hover:bg-yellow-500" v-bind="attrs" v-on="on" >
        <font-awesome-icon class="text-white w-8 h-8" icon="fa-solid fa-list" />
      </button>
      <div v-if="mode=='list'" class="disabled inline-flex bg-teal-600 w-12 h-12 p-2 mr-4 rounded-full" v-bind="attrs" v-on="on" >
        <font-awesome-icon class="text-white w-8 h-8" icon="fa-solid fa-list" />
      </div> -->
      
    </div>
  </nav>
  <div v-if="mode=='board'"><dragTicket></dragTicket></div>
  <div v-if="mode=='table'"><tableTicket></tableTicket></div>
  </div>
</v-app>
</template>

<script>
import addNewTicket from './components/addNewTicket';
import dragTicket from './components/dragTicket';
import tableTicket from './components/tableTicket';

export default {
  name: 'App',

  components: {
    dragTicket,addNewTicket,tableTicket
  },

  data: () => ({
    mode: "board"
  }),
  methods: {
    switchMode(s) {
      this.mode = s
    }
  }
}
</script>

<style>
  body {
    font-family: 'IBM Plex Sans Thai', sans-serif !important;
  }

  @import url('https://fonts.googleapis.com/css2?family=IBM+Plex+Sans+Thai:wght@500&family=Prompt:wght@500&display=swap');
  .dragFont{
    font-family: 'IBM Plex Sans Thai', sans-serif !important;
  }

  .background-animate {
    background-size: 400%;

    -webkit-animation: AnimationName 30s ease infinite;
    -moz-animation: AnimationName 30s ease infinite;
    animation: AnimationName 30s ease infinite;
  }

  @keyframes AnimationName {
    0%,
    100% {
      background-position: 0% 50%;
    }
    50% {
      background-position: 100% 50%;
    }
  }
