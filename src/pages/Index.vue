<template>
  <q-layout view="lHh Lpr lFf">
    <div class="row justify-around q-ma-md">
      <q-btn
        @Click="select(index)"
        :class="card.class+' q-ma-sm'"
        style="width: 6em; height:6em;"
        v-for="(card, index) in cards"
        :key="card.id"
      >
        <q-img class="rounded-borders absolute-full" :src="card.default" />
        <div class="absolute-full rounded-borders bg-blue" v-show="false" />
      </q-btn>
        <q-dialog v-model="show_winner" persistent transition-show="scale" transition-hide="scale">
      <q-card class="bg-positive text-white" style="width: 300px">
        <q-card-section>
          <div class="text-h6">FELICIDADES</div>
        </q-card-section>

        <q-card-section class="q-pt-none">
          !Haz terminado este juego, nos vemos para otra ronda!
        </q-card-section>

        <q-card-actions align="right" class="bg-white text-teal">
          <q-btn @Click="again" flat label="Jugar otra vez" v-close-popup />
        </q-card-actions>
      </q-card>
    </q-dialog>
    </div>
  </q-layout>
</template>

<script>

const defaultImg = 'https://firebasestorage.googleapis.com/v0/b/sename-app.appspot.com/o/card.png?alt=media&token=f31a7909-1065-4f90-a7f1-348992561b9d'

import { defineComponent, ref, computed } from 'vue'
import { useStore } from 'vuex'
export default defineComponent({
  name: 'MainLayout',


  data() {
    const $store = useStore()
    return {
      audioSelect: new Audio('https://firebasestorage.googleapis.com/v0/b/sename-app.appspot.com/o/AUDIOS%2FEffects%2Fpress-intro.mp3?alt=media&token=a8b707a3-f770-4aba-a08e-42b862c49a5d'),
      audioCorrect: new Audio('https://firebasestorage.googleapis.com/v0/b/sename-app.appspot.com/o/AUDIOS%2FEffects%2Fpress-positive.mp3?alt=media&token=e50965e5-deb0-499b-80f8-c167538193ca'),
      audioWrong: new Audio('https://firebasestorage.googleapis.com/v0/b/sename-app.appspot.com/o/AUDIOS%2FEffects%2Fpress-wrong.mp3?alt=media&token=b12f0ea1-3efa-4931-9efb-934dc7794240'),
      autoplay:false,
      show_winner: false,
      card: [],
      cards: [
        {
          id:0,
          default: defaultImg,
          img: 'https://firebasestorage.googleapis.com/v0/b/sename-app.appspot.com/o/chico-bici.jpeg?alt=media&token=80a53193-4790-4f30-a930-8da7bedea184',
          select: false,
          class:""
        },
        {
          id:1,
          default: defaultImg,
          img: 'https://firebasestorage.googleapis.com/v0/b/sename-app.appspot.com/o/comiendo-helado.jpeg?alt=media&token=11a8afb7-4ecf-43f6-9812-18fdac81593a',
          select: false,
          class:""
        },
        {
          id:3,
          default: defaultImg,
          img: 'https://firebasestorage.googleapis.com/v0/b/sename-app.appspot.com/o/jugando-pelota.jpeg?alt=media&token=5b055ae9-33d3-4583-a98d-e410388ba701',
          select: false,
          class:""
        },
        {
          id:2,
          default: defaultImg,
          img: 'https://firebasestorage.googleapis.com/v0/b/sename-app.appspot.com/o/imagenes%2Fballons.jpg?alt=media&token=245ce54f-37e4-4cee-9da6-a91ca9d78f6f',
          select: false,
          class:""
        },
        {
          id:4,
          default: defaultImg,
          img: 'https://firebasestorage.googleapis.com/v0/b/sename-app.appspot.com/o/bebe-animal.jpeg?alt=media&token=925a6ea9-c4a0-4a31-bb18-9cefd84e43d7',
          select: false,
          class:""
        },
        {
          id:5,
          default: defaultImg,
          img: 'https://firebasestorage.googleapis.com/v0/b/sename-app.appspot.com/o/ni%C3%B1os.jpg?alt=media&token=a73fbcc4-0b5f-41f8-bd48-4284a887552e',
          select: false,
          class:""
        },
        {
          id:6,
          default: defaultImg,
          img: 'https://firebasestorage.googleapis.com/v0/b/sename-app.appspot.com/o/chico-bici.jpeg?alt=media&token=80a53193-4790-4f30-a930-8da7bedea184',
          select: false,
          class:""
        },
        {
          id:7,
          default: defaultImg,
          img: 'https://firebasestorage.googleapis.com/v0/b/sename-app.appspot.com/o/comiendo-helado.jpeg?alt=media&token=11a8afb7-4ecf-43f6-9812-18fdac81593a',
          select: false,
          class:""
        },
        {
          id:8,
          default: defaultImg,
          img: 'https://firebasestorage.googleapis.com/v0/b/sename-app.appspot.com/o/jugando-pelota.jpeg?alt=media&token=5b055ae9-33d3-4583-a98d-e410388ba701',
          select: false,
          class:""
        },
        {
          id:11,
          default: defaultImg,
          img: 'https://firebasestorage.googleapis.com/v0/b/sename-app.appspot.com/o/imagenes%2Fballons.jpg?alt=media&token=245ce54f-37e4-4cee-9da6-a91ca9d78f6f',
          select: false,
          class:""
        },
        {
          id:9,
          default: defaultImg,
          img: 'https://firebasestorage.googleapis.com/v0/b/sename-app.appspot.com/o/bebe-animal.jpeg?alt=media&token=925a6ea9-c4a0-4a31-bb18-9cefd84e43d7',
          select: false,
          class:""
        },
        {
          id:10,
          default: defaultImg,
          img: 'https://firebasestorage.googleapis.com/v0/b/sename-app.appspot.com/o/ni%C3%B1os.jpg?alt=media&token=a73fbcc4-0b5f-41f8-bd48-4284a887552e',
          select: false,
          class:""
        }
      ]
    }
  },
  methods: {
    again(){
      this.show_winner = false
      this.card = Array(null)
      this.cards = [
        {
          id:0,
          default: defaultImg,
          img: 'https://firebasestorage.googleapis.com/v0/b/sename-app.appspot.com/o/chico-bici.jpeg?alt=media&token=80a53193-4790-4f30-a930-8da7bedea184',
          select: false,
          class:""
        },
        {
          id:1,
          default: defaultImg,
          img: 'https://firebasestorage.googleapis.com/v0/b/sename-app.appspot.com/o/comiendo-helado.jpeg?alt=media&token=11a8afb7-4ecf-43f6-9812-18fdac81593a',
          select: false,
          class:""
        },
        {
          id:3,
          default: defaultImg,
          img: 'https://firebasestorage.googleapis.com/v0/b/sename-app.appspot.com/o/jugando-pelota.jpeg?alt=media&token=5b055ae9-33d3-4583-a98d-e410388ba701',
          select: false,
          class:""
        },
        {
          id:2,
          default: defaultImg,
          img: 'https://firebasestorage.googleapis.com/v0/b/sename-app.appspot.com/o/imagenes%2Fballons.jpg?alt=media&token=245ce54f-37e4-4cee-9da6-a91ca9d78f6f',
          select: false,
          class:""
        },
        {
          id:4,
          default: defaultImg,
          img: 'https://firebasestorage.googleapis.com/v0/b/sename-app.appspot.com/o/bebe-animal.jpeg?alt=media&token=925a6ea9-c4a0-4a31-bb18-9cefd84e43d7',
          select: false,
          class:""
        },
        {
          id:5,
          default: defaultImg,
          img: 'https://firebasestorage.googleapis.com/v0/b/sename-app.appspot.com/o/ni%C3%B1os.jpg?alt=media&token=a73fbcc4-0b5f-41f8-bd48-4284a887552e',
          select: false,
          class:""
        },
        {
          id:6,
          default: defaultImg,
          img: 'https://firebasestorage.googleapis.com/v0/b/sename-app.appspot.com/o/chico-bici.jpeg?alt=media&token=80a53193-4790-4f30-a930-8da7bedea184',
          select: false,
          class:""
        },
        {
          id:7,
          default: defaultImg,
          img: 'https://firebasestorage.googleapis.com/v0/b/sename-app.appspot.com/o/comiendo-helado.jpeg?alt=media&token=11a8afb7-4ecf-43f6-9812-18fdac81593a',
          select: false,
          class:""
        },
        {
          id:8,
          default: defaultImg,
          img: 'https://firebasestorage.googleapis.com/v0/b/sename-app.appspot.com/o/jugando-pelota.jpeg?alt=media&token=5b055ae9-33d3-4583-a98d-e410388ba701',
          select: false,
          class:""
        },
        {
          id:11,
          default: defaultImg,
          img: 'https://firebasestorage.googleapis.com/v0/b/sename-app.appspot.com/o/imagenes%2Fballons.jpg?alt=media&token=245ce54f-37e4-4cee-9da6-a91ca9d78f6f',
          select: false,
          class:""
        },
        {
          id:9,
          default: defaultImg,
          img: 'https://firebasestorage.googleapis.com/v0/b/sename-app.appspot.com/o/bebe-animal.jpeg?alt=media&token=925a6ea9-c4a0-4a31-bb18-9cefd84e43d7',
          select: false,
          class:""
        },
        {
          id:10,
          default: defaultImg,
          img: 'https://firebasestorage.googleapis.com/v0/b/sename-app.appspot.com/o/ni%C3%B1os.jpg?alt=media&token=a73fbcc4-0b5f-41f8-bd48-4284a887552e',
          select: false,
          class:""
        }
      ]
    },
    select(index) {
      console.log(this.card.img, this.card.length)
      console.log(this.cards, this.card.length)
      this.audioSelect.play()
      if (this.cards[index].select == false) {
        if (this.cards[index].default != this.cards[index].img) {
          this.cards[index].default = this.cards[index].img
          this.card.push(index)
          if (this.card.length == 2) {
            if (this.card[0] == this.card[1]) {
              this.card = ref(null)
            }
            else {
              setTimeout(() => {
                if (this.cards[this.card[0]].img == this.cards[this.card[1]].img) {
                  this.audioCorrect.play()
                  this.cards[this.card[0]].select = true
                  this.cards[this.card[1]].select = true
                    var condicion = true
                    this.cards.forEach((item)=>{
                      if(!item.select){
                        condicion = false
                      }
                    })
                    if(condicion){
                      this.show_winner = true
                    }
                } else {
                  this.audioWrong.play()
                  setTimeout(() => {

                    this.cards[this.card[0]].default = defaultImg
                    this.cards[this.card[1]].default = defaultImg
                  }, 500);
                }
                setTimeout(() => {
                  this.card = []
                }, 500);
                
              }, 1000);

            }
          }
        } else {
          this.cards[index].default = defaultImg
        }
      }

    }
  },
  create() {
    this.cards.sort(() => Math.random() - 0.5)
  }
})

</script>