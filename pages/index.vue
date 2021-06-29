<template>
  <div class="index-page page-container">
 <Header @menuCreated="mountedPlay()"/>

<div class="index-grid">
<div class="red-box">
</div>
<div class="image1">
<img src="@/assets/images/img4.jpg" class="w-full block" alt="">
<p>Personal</p>

  </div>
<div class="image2">
<img src="@/assets/images/img3.jpg" class="w-full block" alt="">
  </div>
<div class="show">
  <section @mouseover="showHover" @mouseleave="showHoverOut">
      <a href="javscript:void(0)" >
<svg  viewBox="0 0 45 6" fill="none" xmlns="http://www.w3.org/2000/svg">
<path d="M45 3L40 0.113249V5.88675L45 3ZM40.5 2.5L0 2.5V3.5L40.5 3.5V2.5Z" fill="white"/>
</svg>
<h4>
  Show</h4></a>
  </section>
</div>
<div class="heading">
  <h1 class="text-red"><span>Photographer</span></h1>
    <h2><span>Portfolio</span></h2>

</div>
<div class="stiven text-red">
  Stiven <span>Lumer</span>
</div>

</div>

  </div>
</template>

<script>

import gsap from 'gsap'
import  CSSRulePlugin  from "gsap/CSSRulePlugin";
import imagesLoaded from 'imagesloaded';

export default {
  data(){
    return{
      menuTL:gsap.timeline(),
      clicked:false
    }
  },
  mounted () {


  },
  methods:{ 
    mountedPlay(){

    imagesLoaded( document.querySelector('.index-page'), function( instance ) {
    gsap.registerPlugin(CSSRulePlugin);
    // gsap.registerPlugin(Flip);
    let rule = CSSRulePlugin.getRule('.image1:after');
    let rule2 = CSSRulePlugin.getRule('.image2:after');
    let rule3 = CSSRulePlugin.getRule('.show:after');

    let tl = gsap.timeline();  

    tl.to('.loader',{delay:1,duration:.5,autoAlpha:0,ease:'power1.out'});
    tl.to(rule2,{duration:.8,cssRule:{scaleY:0},ease:"power4.inOut"})
    tl.from('.image2 img',{duration:.8,scale:1.2,ease:"power2.inOut"},'-=.6');
    tl.from('.heading h1 span',{duration:.8,clipPath:'polygon(0 0, 0% 0, 100% 100%, 100% 100%)',ease:"power4.inOut"},'-=.4')
    tl.to(rule,{duration:.8,cssRule:{scaleY:0},ease:"power4.inOut"},'-=.2')
    tl.from('.image1 img',{duration:.8,scale:1.2,ease:"power2.inOut"},'-=.6')
    tl.from('.red-box',{duration:.5,scaleY:0,ease:"power4.inOut"});
    tl.from(rule3,{duration:.8,cssRule:{scaleX:0},ease:"power4.inOut"})
    tl.from('.show section',{duration:.8,translateX:'100%',ease:"power4.inOut"},'-=.8')
    tl.from('.heading h2 span',{duration:.8,clipPath:'polygon(0 0, 0% 0, 100% 100%, 100% 100%)',ease:"power4.inOut"},'-=.5')
    tl.from('.stiven',{duration:.5,autoAlpha:0,translateY:'50%',ease:"power1.inOut"});

    // tl.from('.stiven',{duration:.5,autoAlpha:0,translateY:"10%",ease:"power2.inOut"})

    // tl.to(rules[0],{duration:2,cssRule:{height:0}});
});

    },
     showHover(){
    let rule3 = CSSRulePlugin.getRule('.show:after');
      gsap.to(rule3,{duration:.5,cssRule:{scaleX:.75}})
    },
    showHoverOut(){
      let rule3 = CSSRulePlugin.getRule('.show:after');
      gsap.to(rule3,{duration:.5,cssRule:{scaleX:1}})
    },
  }
}
</script>

<style lang="scss">
//CSS For Animation Purposes Only

.image1,.image2{
  overflow:hidden;
  width:100%;
  height:100%;
  position:relative;

  img{
    transform:scale(1);
  }
}
.image1{
    &:after{
    content:'';
    position:absolute;
    background:#fff;
    width:100%;
    height:100%;
    top:0;
    left:0;
    right:0;
    bottom:0;
    transform-origin:center top;

  }
}

.image2{
    &:after{
    content:'';
    position:absolute;
    background:#fff;
    width:100%;
    height:100%;
    top:0;
    left:0;
    right:0;
    bottom:0;
    transform-origin:center bottom;

  }
}

//Animation Code Ends




.index-page{
  height:100vh;
  overflow:hidden;
}
.index-grid{
  display:grid;
  /* grid-template-areas:". box . ."
                      ". box image1 stiven"
                      ". image2 image2 image2"
                      "heading heading heading heading"
                      "heading image2 image2 image2"
                      ". image2 image2 image2"
                      ". . show show"; */
    grid-template-columns:repeat(12,1fr);
    grid-template-rows:repeat(16,1fr);
    height:100vh;

}

.heading{
  display:block;
  grid-row:9 / 11;
  grid-column:1 / 13;
  z-index:10;
  text-align:center;
  margin-top:5%;
  h1{
  span{
          clip-path: polygon(0 0, 85% 0, 100% 100%, 15% 100%);
    }
    margin:0;
    font-size:calc(11vw + 1rem);
  }
  h2{
    color:#fff;
    text-align:right;
    padding-right:8%;
    font-size:calc(10.5vw + 1rem);
    span{
        clip-path: polygon(0 0, 80% 0%, 100% 100%, 20% 100%);
    }
  }
}
.stiven{
  display:block;
  grid-row:3 / 4;
  grid-column:11 / 12;
  font-weight:600;
  span{
    margin-left:.75rem;
  }
}
.show{
  z-index:10;
  display:block;
  grid-column:7 / 13;
  grid-row:13 / 17;
  mix-blend-mode:multiply;
  padding:1.2rem;
  font-size:1.5rem;
  color:#fff;
  display:flex;
  justify-content:flex-end;
  align-items:flex-end;
  position:relative;
  &:after{
        transform-origin:center right;
        content:'';
        position:absolute;
        top:0;
        left:0;
        bottom:0;
        right:0;
        width:100%;
        height:100%;
        background:rgb(229, 36, 36,1);
  }
  section{
    z-index:5;
    max-width:60%;
    margin-left:auto;
    h4{
      text-align:right;
    }
  }
}
.image2{
  display:block;
  grid-column:5 / 12;
  grid-row:6 / 15;
  z-index:6;
      margin-left:5%;
    margin-top:10%;
  img{
        height:100%;
    object-fit: cover;
    object-position:top center;


  }
}
.image1{
  position:relative;
  grid-column:4 / 10;
  grid-row:3 / 10;
  // margin-top:15%;
  p{
    z-index:4;
    text-align:center;
    position:absolute;
    color:#fff;
    text-transform: uppercase;
    top:12%;
    left:0;
    right:0;
    font-weight:600;
    font-size:15px;
  }
  img{
    height:100%;
    object-fit: cover;
  }
}

.red-box{
  transform-origin: center top;
  z-index:3;
  background:rgb(229, 36, 36,1);
  mix-blend-mode:multiply;
  grid-column:2 / 7;
  grid-row:1 / 6;
  margin-bottom:18%;
  margin-left:15%;
 /* width:500px;
  height:200px;
  position:absolute; */
}
.page-container{
}
.header-container{
  max-width:88%;
  margin:0 auto;
  position:relative;
  svg{
    color:#E52424;
    //  cursor:pointer;  
  }
}
header{
  padding:1.5rem 0rem;
  top:5%;
  width:100%;
  position:absolute;
  display:flex;
  justify-content: space-between;
  .logo{
    width:1rem;
  }
}
@media only screen and (min-width:1024px){
    header{
      .logo{
    width:1.5rem;
  }
    }
  .loader{
    svg{
      width:15%;
    }
  }
  // .header-container{
  //   max-width:82%;
  // }
  .red-box{
    grid-row:1 / 9;
  }
  .heading{
    margin-top:0;
  }
  .stiven{
    font-size:1.4rem;
  }
  .show{
    grid-column:10 / 16;
  }
}
@media only screen and (min-width:1280px){

.header-container{
      // max-width:82%;
header{
  padding-top:3.4rem;
}

}
.red-box{
  grid-row:1 / 10;
  grid-column:2 / 6;
}
.image1{
  grid-column:4 / 10;
  grid-row:3 / 13;
}
.image2{
  grid-column:5 / 11;
  grid-row:5 / 16;
  
}

}

@media only screen and (min-width:1366px){
  .header-container{
    header{
      padding-top:4rem;
    }
  }
.image1{
  margin-top:1rem;
  grid-row:2 / 13;
  p{
    top:auto;
    bottom:46%;
    left:40%;
    right:auto;
    z-index:10;
  }
}
.image2{
  margin:0;
  margin-left:10%;
  grid-column:5 / 11;
    grid-row:4 / 16;

}
.stiven{
    grid-row:2 / 3;
  grid-column:10 / 11;
  margin-left:40%;
    margin-top:1rem;

}
.red-box{

}
.heading{
  grid-row:7 / 10;
      margin-right:2%;;

  h1{
    font-size:calc(6.5vw + 1rem);
    text-align:right;
    span{

          // clip-path: polygon(0 0, 85% 0, 100% 100%, 15% 100%);
    }
  }
  h2{
    margin-left:25%;
    text-align:left;
    font-size:calc(6.5vw + 0.8rem);

  }
}
.show{
  padding:3.6rem;
  h4{
    margin-top:.75rem;
  }
}
}

@media only screen and (min-width:1800px){
  header{
    .logo{
      width:2rem;
    }
  }
  .header-container{
    max-width:85%;
  }
  .image1{
    grid-column:3 / 8;
    p{
      bottom:45%;
      left:55%;
    }
  }
  .red-box{
    grid-column:2 / 6;
  }
  .image2{
        margin:0;
        grid-row:5 / 16;
        grid-column:5 / 10;
        img{
                  margin:0;
        margin-bottom:5%;
        }
  }
  .stiven{
    margin:0;
    grid-column:9 / 10;
          justify-self:end;
    span{
      display:block;
    }
  }
  .show{
    grid-row:12 / 17;
    grid-column:9 / 17;
    padding:15% 15%;
    section{
          cursor:pointer;
    }
  }

.heading{
  grid-column:1 / 12;
  margin:0;
  h1{
      // margin:0;
  }
  h2{
    margin-left:30%;
  }
}

}
@media only screen and (max-width: 900px) and (orientation:landscape){
  .index-page{
    overflow-y:auto;
  }
  .index-page,.index-grid{
    height:250vh;
  }
}

</style>
