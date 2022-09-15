<template>
  <aside class="quick_menu">
    <div class="unit">
      <a href="tel:02-2055-0296" class="btn_cs"><b class="tel1">전화문의</b><b class="tel2">02.<br/>3486.5116</b></a>
      <a href="http://www.namuasset.com/?page_id=7702&mod=list&pageid=1" target="_blank" class="btn_qna"><b>자주묻는질문</b></a>
      <a href="http://www.namuasset.com/?page_id=5909" target="_blank" class="btn_case"><b>컨설팅사례</b></a>
    </div>
    <button class="btn_top animate__animated" :class="aniInfo.area2 == 'true'?'animate__fadeIn' : 'animate__fadeOut'" @click="fnMoveTop()"><b>TOP</b></button>
    <ChanelTalk/>
  </aside>
</template>

<script>
import ChanelTalk from "~/components/common/ChanelTalk";

export default {
  components: {
    ChanelTalk
  },

  data() {
    return {
      aniInfo:{
        visual: {
          h1:"false",
          h2:"false",
          p:"false",
        },
        area2:"false",
      },
      swiperOption: {
        slidesPerView: 1,
        observer: true,
        observeParents: true,
        loop: true,
        touchRatio: 0,
        autoplay: {
          delay: 6000,
          disableOnInteraction: false
        },
        effect: "fade",
        speed: 300,
        navigation: false,
        pagination: {
          el: ".sw_pagination",
          clickable: true,
        },
      },
    };
  },
  mounted() {
    window.addEventListener("scroll", () => {
      if(this.$route.path == "/"){
        // let target = document.querySelector(".visual").clientHeight/2;
        let target = document.querySelector(".visual").clientHeight;
        if(target < window.scrollY ){
          this.fnEndVisualAni();
        }else{
          if(!document.querySelector(".visual h1.animate__animated").classList.contains("animate__fadeInDown")){
            this.fnStartVisualAni();
          }
        }
        let target2 = (document.querySelector(".area1").offsetTop );
        target2 -= this.$store.state.ui.view == "pc" ? 55 : 0;
        if(window.scrollY > target2){
          this.fnStartAni("area2");
        }else{
          this.fnEndAni("area2");
        }
      }
    });
  },
  methods: {
    fnMoveTop() {
      window.scrollTo({ top: 0, left: 0, behavior: 'smooth' });
    },
    fnStartVisualAni(){
			if(this.aniInfo.visual.h1 == "hide"){
        this.aniInfo.visual.h1 = "false";
        this.aniInfo.visual.h2 = "false";
        this.aniInfo.visual.p = "false";
      }
      this.aniInfo.visual.h1 = "true";
      this.aniInfo.visual.h2 = "true";
      this.aniInfo.visual.p = "true";
    },
    fnEndVisualAni(){
			if(this.aniInfo.visual.h1 == "hide"){
        this.aniInfo.visual.h1 = "false";
        this.aniInfo.visual.h2 = "false";
        this.aniInfo.visual.p = "false";
      }
      this.aniInfo.visual.h1 = "hide";
      this.aniInfo.visual.h2 = "hide";
      this.aniInfo.visual.p = "hide";
    },
    // fnStartAear1Ani
    //animate__bounceIn area3
    //animate__flipInX
    fnStartAni(name){
			if(this.aniInfo[name] == "true") this.aniInfo[name] = "false";
      this.aniInfo[name] = "true";
    },
    fnEndAni(name){
			if(this.aniInfo[name] == "false") this.aniInfo[name] = "true";
      this.aniInfo[name] = "false";
    }
  },  
};
</script>
