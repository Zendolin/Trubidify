<template>
  <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet" />

  <div class="bg-dark h-screen">
    <div class="flex" style="height: 88vh;">
      <!-- side nav -->
      <div class="w-56 bg-black h-full flex-none relative">
        <div class="p-6">
          <img src="./assets/logo_spotify.png"
            class="h-10"
            />
        </div>
        <div class="mx-2">
          <button v-for="page in pages" :key="page.id" @click="setID = page.id" :class="`w-full focus:outline-none text-xs font-semibold rounded px-3 py-2 flex items-center justify-start ${setID === page.id ? 'bg-light text-white' : 'text-lightest'}`">
            <i class="material-icons mr-3"> {{page.icon}} </i>
            <p> {{ page.name }} </p>
          </button>
        </div>
        <div class="mx-5">
          <h1 class="mb-3 text-xs text-lightest tracking-widest uppercase">Playlists</h1>
          <button class="flex items-center justify-start opacity-75 hover:opacity-100 mb-2">
            <img src="./assets/addNew.png" class="h-8 w-8 mr-3"/>
            <p class="text-sm text-white font-semibold">Créer une playlist</p>
          </button>
          <button class="flex items-center justify-start opacity-75 hover:opacity-100">
            <img src="./assets/favorites.png" class="h-8 w-8 mr-3"/>
            <p class="text-sm text-white font-semibold">Titres likés</p>
          </button>
          <div class="h-px w-full bg-light my-3">
          </div>
        </div>
        <div class="mx-5">
          <div class="w-full h-10 mb-2 overflow-y-scroll">
            <p v-for="playlist in playlists" :key="playlist.name" class="text-lightest hover:text-white text-xs py-2">{{ playlist.name }}</p>
          </div>
          <button class="flex items-center justify-star text-lightest hover:text-white">
            <i class="material-icons mr-3 rounded-full border border-lightest" style="font-size: 18px;">arrow_downward</i>
            <p class="text-sm font-semibold">Installer l'appli</p>
          </button>
        </div>

        <div class="absolute bottom-0">
          <div class="relative pt-4">
            <div class="w-full h-full flex justify-end items-start absolute p-2 opacity-0 hover:opacity-100">
              <div class="bg-black rounded-full h-6 w-6">
                <i class="material-icons text-white">keyboard_arrow_down</i>
              </div>
            </div>
            <img class="w-full" src="./assets/song.png" />
          </div>
        </div>
        
        
      </div>
      <!-- main content -->
      <div class="w-full h-full relative overflow-y-scroll">
        <!-- header -->
        <div class="w-full sticky top-0 py-3 px-5 flex items-center justify-between bg-dark">
          <div class="flex items-center">
            <button class="rounded-full bg-black w-8 h-8 text-white mr-3">
              <i class="material-icons" style="font-size: 30px;">keyboard_arrow_left</i>
            </button>
            <button class="rounded-full bg-black w-8 h-8 text-white mr-3">
              <i class="material-icons" style="font-size: 30px;">keyboard_arrow_right</i>
            </button>
          </div>

          <div class="relative">
            <button @click="showDropdown = !showDropdown" class="bg-light rounded-full py-1 px-2  flex items-center">
              <img src="./assets/pictureProfile.png" class="rounded-full h-6 w-6 mr-2"/>
              <p class="text-white text-xs mr-3 font-semibold">Zendolin</p>
              <i v-if="showDropdown === false" class="material-icons text-white">arrow_drop_down</i>
              <i v-if="showDropdown === true" class="material-icons text-white">arrow_drop_up</i>
            </button>
            <div v-if="showDropdown === true" class="absolute bg-light w-full rounded mt-1">
              <button @click="showDropdown = false" class="w-full focus:outline-none py-2 text-sm text-lightest hover:text-white border-b border-lightest">Compte</button>
              <button @click="showDropdown = false" class="w-full focus:outline-none py-2 text-sm text-lightest hover:text-white">Déconnexion</button>
            </div>
          </div>

        </div>

        <!-- cards -->
        <div class=" px-6 py-3">
          <div class="flex items-center justify-between">
            <h1 class="text-2xl font-bold text-white hover:underline">Écoutés récemment</h1>
            <h2 class="text-xs pt-4 text-lightest tracking-wider uppercase hover:underline mb-3">Voir Tout</h2>
         
          </div>
          <div class="w-full flex flex-wrap">
            <div v-for="recent in recents" :key="recent.artist" class="p-2 w-48 relative">
              <div class="w-full h-full p-8 flex items-end justify-end absolute opacity-0 hover:opacity-100">
                <div class="bg-green rounded-full h-8 w-8">
                  <i class="material-icons text-white" style="font-size: 32px;">play_arrow</i>
                </div>
              </div>
              <div class="bg-light w-full h-auto p-5 rounded-lg shadow-md">
                <img :src="`${recent.src}`" class="h-auto w-full shadow mb-2" />
                <h1 class="text-sm font-semibold text-white tracking-wide">{{ recent.title }}</h1>
                <h2 class="text-xs text-lightest tracking-wide mb-4">{{ recent.artist }}</h2>
              </div>

            </div>
          </div>
        </div>

        <div class=" px-6 py-3">
          <div class="">
            <h1 class="text-2xl font-bold text-white hover:underline">Créer pour Zendolin</h1>
            <div class="flex items-center justify-between">
              <h3 class=" text-sm text-lightest">Plus vous écoutez, plus les recommandations s'améliorent.</h3>
              <h2 class="text-xs pt-4 text-lightest tracking-wider uppercase hover:underline">Voir Tout</h2>
            </div>
          </div>

          <div class="w-full flex flex-wrap">
            <div v-for="custom in customs" :key="custom.artist" class="p-2 w-48 relative">
              <div class="w-full h-full p-8 flex items-end justify-end absolute opacity-0 hover:opacity-100">
                <div class="bg-green rounded-full h-8 w-8">
                  <i class="material-icons text-white" style="font-size: 32px;">play_arrow</i>
                </div>
              </div>
              <div class="bg-light w-full h-auto p-5 rounded-lg shadow-md">
                <img :src="`${custom.src}`" class="h-auto w-full shadow mb-2" />
                <h1 class="text-sm font-semibold text-white tracking-wide">{{ custom.title }}</h1>
                <h2 class="text-xs text-lightest tracking-wide mb-4">{{ custom.artist }}</h2>
              </div>

            </div>
          </div>
        </div>
        


      </div>
    </div>

    <!-- play bar -->
    <div class="w-full flex items-center justify-between px-3 bg-light" style="height: 12vh;">
      <div class="flex items-center justify-start w-1/4">
        <div class="mr-2">
          <h1 class="text-sm text-white font-semibold">Erothyme</h1>
          <h2 class="text-xs text-white">Cherry Picking</h2>
        </div>
        <i class="material-icons text-green mx-4" style="font-size: 20px;">favorite</i>
        <i class="material-icons text-lightest hover:text-white" style="font-size: 20px;">picture_in_picture_alt</i>
      </div>

      <div class="flex flex-col justify-center w-2/4 items-center">
        <div class="flex items-center">
          <button class="text-lightest hover:text-white mx-4 focus:outline-none">
            <i class="material-icons" style="font-size: 20px;">shuffle</i>
          </button>
          <button class="text-lightest hover:text-white focus:outline-none">
            <i class="material-icons" style="font-size: 20px;">skip_previous</i>
          </button>
          <button @click.prevent="pause = !pause; playSong(pause);" class="text-lightest hover:text-white rounded-full flex items-center justify-center h-10 w-10 mx-5 border border-lightest focus:outline-none">
            <i v-if="pause === true" class="material-icons" style="font-size: 20px;">play_arrow</i>
            <i v-if="pause === false" class="material-icons" style="font-size: 20px;">pause</i>
          </button>
          <button class="text-lightest hover:text-white focus:outline-none">
            <i class="material-icons" style="font-size: 20px;">skip_next</i>
          </button>
          <button class="text-lightest hover:text-white mx-4 focus:outline-none">
            <i class="material-icons" style="font-size: 20px;">repeat</i>
          </button>
        </div>

        <div class="w-3/4 flex items-center justify-center mt-3">
          <p class="text-xs text-lightest mr-1">0:28</p>
          <div class="w-full h-1 bg-dark rounded-full flex items-center">
              <div class="h-1 rounded-full bg-green" style="width: 18%;"></div>
              <div class="h-3 w-3 rounded-full bg-white -ml-1"></div>                
          </div>
          <p class="text-xs text-lightest ml-1">3:33</p>
        </div>
      </div>

      <div class="flex items-center w-1/4 justify-end">
        <i class="material-icons text-lightest hover:text-white" style="font-size: 20px;"> playlist_play</i>
        <i class="material-icons text-lightest mx-3 hover:text-white" style="font-size: 20px;">important_devices</i>
        <i class="material-icons text-lightest hover:text-white" style="font-size: 20px;">volume_up</i>
        <div class="w-20 m-1 h-1 bg-lightest rounded-full"></div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  components: {
  },
  data: function() {
    return{
      pages: [
        {id: 'home', name:'Accueil', icon: 'home'},
        {id: 'search', name:'Rechercher', icon: 'search'},
        {id: 'library', name:'Bibliothèque', icon: 'bar_chart'}
      ],
      setID: 'home',
      playlists: [
        {name: 'Vos Top titres en 2019'},
        {name: 'Vos titres préférés de 2020'},
        {name: "K/DA"},
        {name: "Red Velvet"},
        {name: "Outrun"},
        {name: 'Japan'}
      ],
      showDropdown: false,
      recents: [
        {src: "song1.jpg", title: "Into Memory", artist: "Canada Panic"},
        {src: "song2.jpg", title: "Lazy Legend", artist: "Frank Le"},
        {src: "song6.png", title: "Dance Moments", artist: "Ayisha Tate"},
        {src: "song4.jpg", title: "Sleep In Noise", artist: "Teddy Bear Tribute"},
        {src: "song5.jpg", title: "Recline Tango", artist: "Giles Beard"}
      ],
      customs: [
        {src: "discover.jpg", title: "Découverte de la ...", artist: "Par Spotify"},
        {src: "dm1.jpg", title: "Daily Mix 1", artist: "Par Spotify"},
        {src: "dm2.jpg", title: "Daily Mix 2", artist: "Par Spotify"},
        {src: "dm3.jpg", title: "Daily Mix 3", artist: "Par Spotify"},
        {src: "dm4.jpg", title: "Daily Mix 4", artist: "Par Spotify"}
      ],
      pause: true,
      audio: new Audio('song.mp3')
    };
  },
  methods: {
    playSong(pause){

      if(pause){
        this.audio.pause();
      }
      else{
        this.audio.play();
      }
      
      
    }
  }
};
</script>