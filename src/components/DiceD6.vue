
<template>
     <div class="playground" :style="styles['playground']">
    <div :id="id" class="dice" :dice="classDice" :style="[styles['dice'], { left: fixedPosition }]"
      @click="rollIsDone ? rollDice(getRndInteger(1, 6)) : null">
      <div class="cube-face d-flex justify-content-center align-items-center" :class="allFaces.cubeFace1"
        :style="[styles['cube-face'], styles['cube-face-1']]" v-if="allFaces.cubeFace1.active">
        <i class="fa-solid fa-circle d-flex justify-content-center align-items-center m-2"
          :style="styles['cube-face-i']"></i>
      </div>
      <div class="cube-face d-flex justify-content-center align-items-center" :class="allFaces.cubeFace2"
        :style="[styles['cube-face'], styles['cube-face-2']]" v-if="allFaces.cubeFace2.active">
        <i class="fa-solid fa-circle d-flex justify-content-center align-items-center align-self-start m-2"  v-for="(v,i) in 2" :key="i" :class="{ 'align-self-start': i === 0, 'align-self-end': i !== 0 }"
          :style="styles['cube-face-i']"></i>
      </div>
      <div class="cube-face d-flex justify-content-center align-items-center" :class="allFaces.cubeFace3"
        :style="[styles['cube-face'], styles['cube-face-3']]" v-if="allFaces.cubeFace3.active">
        <i class="fa-solid fa-circle d-flex justify-content-center align-items-center"
          :style="[styles['cube-face-3-5-6-i'], styles['cube-face-i']]" v-for="(v,i) in 3" :key="i" :class="{ 'align-self-start': i === 0, 'align-self-end': i === 2}"></i>
      </div>
      <div class="cube-face d-flex justify-content-center align-items-center flex-wrap"
        :class="allFaces.cubeFace4" :style="[styles['cube-face'], styles['cube-face-4']] "
        v-if="allFaces.cubeFace4.active">
        <i class="fa-solid fa-circle d-flex justify-content-center align-items-center"
          :style="[styles['cube-face-4-i'], styles['cube-face-i']]" v-for="(v,i) in 4" :key="i"></i>
      </div>
      <div class="cube-face d-flex justify-content-around  align-items-center flex-wrap"
        :class="allFaces.cubeFace5" :style="[styles['cube-face'], styles['cube-face-5']]"
        v-if="allFaces.cubeFace5.active">
        <i class="fa-solid fa-circle d-flex justify-content-center align-items-center"
          :style="[styles['cube-face-3-5-6-i'], styles['cube-face-i']]" v-for="(v,i) in 5" :key="i" :class="{'w-100': i === 2}"></i>
      </div>
      <div class="cube-face d-flex justify-content-around  align-items-center flex-wrap"
        :class="allFaces.cubeFace6" :style="[styles['cube-face'], styles['cube-face-6']]"
        v-if="allFaces.cubeFace6.active">
        <i class="fa-solid fa-circle d-flex justify-content-center align-items-center"
          :style="[styles['cube-face-3-5-6-i'], styles['cube-face-i']]" v-for="(v,i) in 6" :key="i"></i>
      </div>
    </div>
  </div>
  </template>


  
  <script>
  import '@fortawesome/fontawesome-free/css/all.css';
  import 'bootstrap/dist/css/bootstrap.min.css';

  export default {
    name: 'DiceD6',
    props: {
      id: {
        type: String,
        default: 'defaultId'
      },
      classDice: {
        type: String,
        default: 'defaultClass'
      },
      dimension: {
        type: Number,
        default: 100
      },
      color: {
        type: String,
        default: 'red'
      },
      dotColor: {
        type: String,
        default: 'black'
      },
      animationDuration: {
        type: Number,
        default: 4000
      }
    },
  
    data() {
      return {
        rollResult: 1,
        allFaces: {
          cubeFace1: { value: 1, active: true },
          cubeFace2: { value: 2, active: false },
          cubeFace3: { value: 3, active: false },
          cubeFace4: { value: 4, active: false },
          cubeFace5: { value: 5, active: false },
          cubeFace6: { value: 6, active: false }
        },
        rollIsDone: true
      };
    },
  
    computed: {
      styles() {
            return {
                'playground': {
                    height: this.dimension + 'px',
                    width: this.dimension + 'px',
                    margin: this.dimension / 2 + 'px',
                },
                'dice': {
                },
                'cube-face': {
                    height: this.dimension + 'px',
                    width: this.dimension + 'px',
                    border: '1px solid black',
                    'border-radius': this.dimension / 8 + 'px',
                    'background-color': this.color,
                },
                'cube-face-i': {
                    height: this.dimension / 4 + 'px',
                    width: this.dimension / 4 + 'px',
                    'font-size': this.dimension * 0.16 + 'px',
                    color: this.dotColor,
                },
                'cube-face-3-5-6-i': {
                    margin: this.dimension * 0.04 + 'px',
                },
                'cube-face-4-i': {
                    margin: this.dimension * 0.08 + 'px',
                },
                'cube-face-1': {
                    transform: `translateZ(${this.dimension / 2}px)`,
                },
                'cube-face-2': {
                    transform: `rotateX(-180deg) translateZ(${this.dimension / 2}px)`,
                },
                'cube-face-3': {
                    transform: `rotateY(90deg) translateZ(${this.dimension / 2}px)`,
                },
                'cube-face-4': {
                    transform: `rotateY(-90deg) translateZ(${this.dimension / 2}px)`,
                },
                'cube-face-5': {
                    transform: `rotateX(90deg) translateZ(${this.dimension / 2}px)`,
                },
                'cube-face-6': {
                    transform: `rotateX(-90deg) translateZ(${this.dimension / 2}px)`,
                },
            };
        },

        fixedPosition() {
            if (this.rollResult===3 || this.rollResult===4) {
                return this.dimension / 4 + 'px'; // Sposta a sinistra
            } else {
                return '0px'; // Nessuno spostamento
            }
        },
        
},

    methods: {
        rollDice(result) {        
            this.enableAllFaces()
            return new Promise((resolve, reject) => {
                this.rollIsDone = false
                let xRandom;
                let yRandom;
                this.rollResult = result;
                if (result === 1) {
                    xRandom = 360 * this.getRndInteger(4, 18);
                    yRandom = 360 * this.getRndInteger(4, 18);
                } else if (result === 2) {
                    xRandom = 180 + (360 * this.getRndInteger(4, 18));
                    yRandom = 360 * this.getRndInteger(4, 18);
                } else if (result === 3) {
                    //this.styles['dice'].left = `${this.dimension / 4}px`;
                    xRandom = 360 * this.getRndInteger(4, 18);
                    yRandom = 270 + (360 * this.getRndInteger(4, 18));
                } else if (result === 4) {
                    // this.dice.style = `left:${this.dimension / 4}px`;s
                    xRandom = 360 * this.getRndInteger(4, 18);
                    yRandom = 90 + (360 * this.getRndInteger(4, 18));
                } else if (result === 5) {
                    xRandom = 270 + (360 * this.getRndInteger(4, 18));
                    yRandom = 360 * this.getRndInteger(4, 18);
                } else {
                    xRandom = 90 + (360 * this.getRndInteger(4, 18));
                    yRandom = 360 * this.getRndInteger(4, 18);
                }
                this.styles['dice'].transition = `transform ${this.animationDuration / 1000}s`;
                this.styles['dice'].transform = `rotateX(${xRandom}deg) rotateY(${yRandom}deg)`;
                setTimeout(() => {
                    this.rollIsDone = true;
                    this.disableAllFaces();
                }, this.animationDuration)
                resolve(); // Risolve la Promise quando l'animazione è completata
            });
        },
        enableAllFaces(){
            for (const faceKey in this.allFaces) {
                this.allFaces[faceKey].active = true;
        }},
        disableAllFaces(){
            for (const i in this.allFaces) {
                this.allFaces[i].value !== this.rollResult ? this.allFaces[i].active = false : "";
            }
        },
        getRndInteger(min, max) {
            return Math.floor(Math.random() * (max - min + 1)) + min;
        },
    }
};
  </script>
  
  <style lang="scss" scoped>
    $spacer: 1rem;
  .playground {
    position: relative;
    perspective: 1000px;
    perspective-origin: 50% 100%;
  }

  .dice {
    height: 100% ;
    width: 50% ;
    position: absolute;
    transform-style: preserve-3d;
  }

  .cube-face {
    display: flex;
    position: absolute;
    margin: 0 auto;
    border: 1px solid rgb(0, 0, 0);
    box-shadow: 0 0 10 5 rgba(255, 255, 255, 0.7);
    cursor: pointer;
  }

  // .d-flex{
  //   display: flex;
  // }

  // .justify-content-center{
  //   justify-content: center;
  // }

  // .justify-content-around{
  //   justify-content: space-around;
  // }

  // .align-items-center{
  //   align-items: center;
  // }

  // .flex-wrap{
  //   flex-wrap: wrap;
  // }

  // .m-2{
  //   margin: $spacer *.5;
  // }

  // .align-self-start {
  //   align-self: flex-start;
  // }

  // .align-self-end {
  //   align-self: flex-end;
  // }

  // .w-100{
  //   width: 100%;
  // }
  </style>
  