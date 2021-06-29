<template>
<div class="main-header">
<Loader/>
          <div class="header-container">
<!-- Menu Start  -->
      <div class="overlay-menu">


<div class="menu-grid">

<p class="menu-text">menu</p>
<div class="img1">
<img src="@/assets/images/menu1.jpg" class="w-full">

</div>

<div class="img2">
<img src="@/assets/images/menu2.jpg" class="w-full">

</div>
<div class="menu-redbox"></div>
<div class="menu-redbox2"></div>

<div class="menu-links">

<ul>

<li class="active"> 

<section class="icon"> <span class="num">01</span><span class="arrow">

<svg  viewBox="0 0 48 6" xmlns="http://www.w3.org/2000/svg"  fill="currentColor">
<path d="M48 3L43 0.113249V5.88675L48 3ZM43.5 2.5L0 2.5V3.5L43.5 3.5V2.5Z"/>
</svg>

</span> </section>
<div class="link">
<a href="#">

<span>
Home</span></a></div></li>
<li ><section class="icon"> <span class="num">02</span><span class="arrow">

<svg  viewBox="0 0 48 6" xmlns="http://www.w3.org/2000/svg">
<path d="M48 3L43 0.113249V5.88675L48 3ZM43.5 2.5L0 2.5V3.5L43.5 3.5V2.5Z" fill="currentColor"/>
</svg>

</span> </section> <div class="link">
<a href="#"><span>About</span></a></div></li>
<li> 
<section class="icon"> <span class="num">03</span><span class="arrow">

<svg  viewBox="0 0 48 6" xmlns="http://www.w3.org/2000/svg">
<path d="M48 3L43 0.113249V5.88675L48 3ZM43.5 2.5L0 2.5V3.5L43.5 3.5V2.5Z" fill="currentColor"/>
</svg>

</span> </section>
<div class="link">
<a href="#">
<span>Gallery</span></a></div></li>
<li> 
<section class="icon"> <span class="num">04</span><span class="arrow">

<svg  viewBox="0 0 48 6" xmlns="http://www.w3.org/2000/svg">
<path d="M48 3L43 0.113249V5.88675L48 3ZM43.5 2.5L0 2.5V3.5L43.5 3.5V2.5Z" fill="currentColor"/>
</svg>

</span> </section>
<div class="link">
<a href="#">
<span>Contact</span></a></div></li>


</ul>

</div>




</div>



      </div>
        <!-- Menu End -->
    <header>


        
        
        
        <nuxt-link to="/" style="color:inherit;">

      <div  class="logo" @mouseover="logoHover($event)" @mouseleave="logoHoverOut($event)">
        <svg  viewBox="0 0 20 25"  xmlns="http://www.w3.org/2000/svg">
          <path d="M0 20H17.5L20 25H2.5L0 20Z" fill="currentColor" />
          <path d="M0 0H17.5L20 5H2.5L0 0Z" fill="currentColor" />
          <path d="M17.5 10L12.5 10L15 5L20 5L17.5 10Z" fill="currentColor" />
          <path d="M5 20H0L2.5 15H7.5L5 20Z" fill="currentColor" />
        </svg>
      </div>
              </nuxt-link>
      <div class="menu-icon">
        <a href="" @click.prevent="openMenu()" >
<svg width="40" height="15" viewBox="0 0 40 15" fill="none" xmlns="http://www.w3.org/2000/svg">
<path d="M0 0H40V4H0V0Z" fill="#E52424"/>

<path d="M15 11H40V15H15V11Z" id="menu2" fill="#E52424"/>
</svg>
</a>
      </div>
    </header>
          </div>

</div>
</template>

<script>
import gsap from 'gsap'
import  CSSRulePlugin  from "gsap/CSSRulePlugin";
export default {
    data(){
        return{

            menuTL:gsap.timeline(),
            clicked:false,

        }
    },
    mounted(){
      this.$emit('menuCreated');
    },
    methods:{
          logoHover(e){
      gsap.to('.logo svg',{duration:.2,color:'#000000',ease:"power4.in"})

    },
    logoHoverOut(e){
      gsap.to('.logo svg',{duration:.2,color:'#E52424',ease:"power4.out"})
    },
 
    openMenu(){
        gsap.registerPlugin(CSSRulePlugin);
    if(this.clicked==false){
           this.clicked = true;
           if(this.menuTL.paused()){
             this.menuTL.play();
           }else{
        //  this.menuTL = gsap.timeline();
         let rule = CSSRulePlugin.getRule('.overlay-menu .img1:after');
         let rule2 = CSSRulePlugin.getRule('.overlay-menu .img2:after');
         this.menuTL.set('.overlay-menu',{display:'block'})
         this.menuTL.to('.overlay-menu',{duration:1,translateY:0,ease:'power4.inOut'});
         this.menuTL.to(rule,{duration:.8,cssRule:{scaleY:0},ease:"power4.inOut"})
         this.menuTL.from('.overlay-menu .img1 img',{duration:.5,scale:1.4,ease:'power2.inOut'},'-=.6');
         this.menuTL.to(rule2,{duration:.8,cssRule:{scaleY:0},ease:"power4.inOut"})
         this.menuTL.from('.overlay-menu .img2 img',{duration:.5,scale:1.2,ease:'power2.inOut'},'-=.6');
         if(window.innerWidth>768){
         this.menuTL.from('.menu-redbox2 ',{duration:.5,transformOrigin:'center right',scaleX:0,ease:'power4.inOut'});
         }
         this.menuTL.from('.menu-redbox ',{duration:.5,transformOrigin:'center bottom',scaleY:0,ease:'power4.inOut'});
         this.menuTL.from('.menu-links ul li ',{duration:.5,stagger:0.2,autoAlpha:0,translateY:'10%',ease:'power4.inOut'});
         this.menuTL.from('.menu-text',{duration:.5,autoAlpha:0,translateY:'10%',ease:'power2.inOut'});
           }
      }else{
        let tl = gsap.timeline();
        tl.to('.overlay-menu',{duration:.6,scaleY:1.2,ease:'power2.inOut'});
        tl.to('.overlay-menu',{duration:1,translateY:'-120%',ease:'power3.inOut'},'-=.5').add(()=>{
          gsap.set('.overlay-menu',{translateY:'-100%',scaleY:1});
                  this.menuTL.seek(0).pause();
        })



        this.clicked=false;

//         alert("Reverse");
      //  this.clicked = false;
//       if (this.menuTL.reversed()) {
//     this.menuTL.play();
// } else {
//     this.menuTL.reverse();
// }
      }
    }
    }
}
</script>