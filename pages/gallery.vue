<template>
    <div class="gallery-page page-container">
 <Header @menuCreated="mountedPlay()"/>


<div class="red-center"></div>

<div class="gallery-grid">

<div class="image first-col">
    <img src="@/assets/images/gallery/img1.jpg" class="w-full" alt="">
</div>
<div class="image second-col">
    <img src="@/assets/images/gallery/img2.jpg" class="w-full" alt="">
</div>
<div class="image third-col">
    <img src="@/assets/images/gallery/img3.jpg" class="w-full" alt="">
</div>
<!-- 
<div class="image alt-img">
    <img src="@/assets/images/gallery/img1.jpg" class="w-full" alt="">
</div> -->


</div>

        </div>
</template>

<script>
import gsap from 'gsap'
import  CSSRulePlugin  from "gsap/CSSRulePlugin";
import imagesLoaded from 'imagesloaded';
import Scrollbar from 'smooth-scrollbar';

import OverscrollPlugin from 'smooth-scrollbar/plugins/overscroll';

export default {
    data(){
        return{

        }
    },
      mounted () {
  Scrollbar.use(OverscrollPlugin)
  Scrollbar.init(document.body, { damping: 0.05, delegateTo: document,plugins:{'overscroll':{'effect':'bounce',damping:0.1}}});
  console.log(Scrollbar);
    },
    methods:{
     mountedPlay(){
          imagesLoaded( document.querySelector('.gallery-page'), function( instance ) {
        gsap.registerPlugin(CSSRulePlugin);
        gsap.to('.loader',{delay:1,duration:.5,autoAlpha:0,ease:'power1.out'});

    
    });

     }

        
    }
}
</script>

<style lang="scss" scoped>

.gallery-grid{
    max-width:88%;
    margin:0 auto;
}
.red-center{
    width:18%;
    background:rgb(229, 36, 36,1);
    position:fixed;
    height:100%;
    left:0;
    right:0;
    top:0;
    bottom:0;
    margin-left:auto;
    margin-right:auto;
    mix-blend-mode:multiply;
}
.gallery-grid{
    padding-top:15%;
    // display:flex;
    display:grid;
    grid-template-columns:repeat(12,1fr);
   .first-col{
        z-index:-1;
        grid-column:1 / 8;
        grid-row:1 / 2;

    }
    .second-col{
        z-index:3;
        grid-column:7 / 13;
        padding-top:50%;
        grid-row:1 / 3;

    }
    .third-col{
        z-index:3;
        grid-column:1 / 8;
        padding-top:100%;
        grid-row:1 / 3;

    }
 
}
@media only screen and (min-width:1024px){
    .gallery-grid{
        max-width:85%;
    }
}

@media only screen and (min-width:1366px){
    .gallery-grid{
        max-width:82%;
    }
}

@media only screen and (min-width:1800px){
    .gallery-grid{
        max-width:70%;
    }
}
</style>