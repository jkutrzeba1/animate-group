<template>
  <transition-group :move-class="smoothMove ? 'animate__move' : ''" @enter="animateCSS($event, 'in')" @leave="animateCSS($event, 'out')">
    <slot></slot>
  </transition-group>
</template>

<script>
  export default {
    props: {
      animationIn: {
        type: String,
        required: true
      },
      animationOut: {
        type: String,
        required: true
      },
      animationDuration: {
        type: Number
      },
      /*
        Specifies whether surrounding elements will occupy placement of inserted/removed element in smoothly way.
        Animate change of position in list.
      */
      smoothMove: {
        type: Boolean,
        default: true
      },
      /*
        Instant move of surrounding elements on leave transition - removed element will be detached from normal document flow - by set its position to absolute.
        Surrounding elements will be moved immediately - rather when animation ends.
        Applied only for out transition
      */
      instantMove: {
        type: Boolean,
        default: true
      }
    },
    data: ()=>({
      animationPrefix: "animate__"
    }),
    methods: {
      animateCSS (element, type){
        return new Promise((resolve) => {
          let animationName;

          if(type==="in"){
            animationName = this.animationIn;
          }
          else if(type==="out"){
            animationName = this.animationOut;
          }

          const classAnimationName = `${this.animationPrefix}${animationName}`;

          if(this.instantMove && type==="out"){
            element.style.position = "absolute";
          }

          if(this.animationDuration){
            element.style.setProperty('--animate-duration', `${this.animationDuration}s`);
          }

          element.classList.add(`${this.animationPrefix}animated`, classAnimationName);

          // When the animation ends, we clean the classes and resolve the Promise
          function handleAnimationEnd() {

            if(this.instantMove && type==="out"){
              element.style.position = "static";
            }

            if(this.animationDuration){
              element.style.removeProperty('--animate-duration', `${this.animationDuration}s`);
            }

            element.classList.remove(`${this.animationPrefix}animated`, classAnimationName);

            resolve('Animation ended');
          }

          element.addEventListener('animationend', handleAnimationEnd, {once: true});
        });
      }
    }
  }
</script>

<style src="animate.css"></style>
<style>
.animate__move {
  transition: transform 1.2s ease;
}
</style>
