<template>
  <div >
    <div class="row" >
      <play-video
        :video="videoData"
        class="col-lg-8"
      />
    </div>

    <div       
      v-if="playList.length"
      class="row"
    >
      <div
        v-for="(item, index) in playList"        
        :key="index"
        class="col-sm-2 col-xs-1 col-lg-2 "
         
      >
   
      <div class="tooltip-movie card"> 
      
            <img class="card-img" :src="item.image" @click="setVideoData(item)"> 
            <span class="tooltiptext"> {{item.description}}</span> 
            </div>
    </div>
     
    </div>
  </div>


</template>
<script>
import MovieServices from "../services/MovieServices.js";
import PlayVideo from "./PlayVideo";

export default {
  name: "App",
  components: {
    PlayVideo,
  },
  data() {
    return {
      playList: [],
      videoData: "",
    };
  },
  created() {
    this.getPlayList();
  },
  methods: {
    getPlayList() {
      MovieServices.getPlayList()
        .then((response) => {
          if (response.data) {
            this.playList = response.data;
             
            console.log(this.playList);
          }
        })
        .catch((e) => {
          console.log(e);
        });
    },
    setVideoData(videoToPlay) {
      this.videoData = videoToPlay.video;
    },
  },
};
</script>

<style scoped>
.tooltip-movie {
  position: relative;
  display: inline-block;
  border-bottom: 1px dotted black;
   
}
img{
      cursor: pointer;
}
.tooltip-movie .tooltiptext {
  
  visibility: hidden;
  width: 200px;
  background-color: grey;
  color: #fff;
  text-align:start;
  border-radius: 6px;
  padding: 5px;

  /* Position the tooltip */
  position: absolute;
  z-index: 1;
}

.tooltip-movie:hover .tooltiptext {
  visibility: visible;
}

@media screen and (max-width:700px){
  
   
}
 
</style>