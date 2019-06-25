<template>
    <div class="keychain" :style="'width:' + keychainWidth + 'cm; height:' + keychainHeight + 'cm;'">
      <div class="upper-left"></div>
      <div class="upper-right"></div>
      <div class="bottom-left"></div>
      <div class="bottom-right"></div>
      <div :style="'height:'+marginButtom+'cm; width:'+keychainWidth+'cm'"></div>
      <div class="qr-code-container" :style="'transform: scale(' + qrScale + '); margin-bottom:-'+(qrWidth-qrWidth*qrScale)/2+'px'">
        <img class="qr-code" :style="'width:' + qrWidth + 'px'" :src="'https://api.qrserver.com/v1/create-qr-code/?size=300x300&data='+data(code)+'&ecc=H&format=svg'" alt="" title="" />
        <div class="logo logo-background" :style="'width:' + logoBGSize + 'px; height:' + logoBGSize + 'px;'">
          <div class="logo-background-qr-dot" :style="'width:' + logoBGSize/7 + 'px; height:' + logoBGSize/7 + 'px; background-color:'+dotColor(dot.show)" v-for="dot in dots" :key="dot.id"></div>
        </div>
        <img class="logo" :style="'width:' + logoWidth + 'px'" alt="Vue logo" :src="logoSrc==''?'logo.png':logoSrc">
      </div>
      <div class="keychain-string" :style="'font-size:' + stringSize + 'pt; margin-bottom:-'+(qrWidth-qrWidth*qrScale)/2+'px;'">ID: {{code}}</div>
      <div class="keychain-title" :style="'font-size:' + titleSize + 'pt; margin-bottom:' + titleMarginBottom + 'cm'" >{{title}}</div>
      <img class="title-logo" :style="'width:' + titleLogoWidth + 'px; margin-bottom:'+titleLogoMarginBottom+'cm'" alt="Vue logo" :src="titleLogoSrc==''?'logo.png':titleLogoSrc">
    </div>
</template>

<script>
export default {
  props: [
    'keychainWidth',
    'keychainHeight',
    'qrWidth',
    'qrScale',
    'logoSrc',
    'logoWidth',
    'titleLogoSrc',
    'titleLogoWidth',
    'marginButtom',
    'title',
    'titleSize',
    'titleMarginBottom',
    'titleLogoMarginBottom',
    'stringSize',
    'dataGymID',
    'code',
    'dots'
    ],
  data(){
    return{

    }
  },
  computed:{
    logoBGSize(){
      return this.qrWidth*7/29
    }
  },
  methods:{
    setLogo(ev){
      if(ev.target.files && ev.target.files[0]){
        const file = ev.target.files[0]
        const reader = new FileReader()
        reader.onload = e => {
          // console.log('reader', e.target.result)
          this.logoSrc = e.target.result
        }
        reader.readAsDataURL(file)
      } else {
        this.logoSrc =''
      }      
    },
    dotColor(condition){
      if(condition){
        return 'white'
      } else {
        return 'transparent'
      }
    },
    data(code){
      return '{"obj":"l","'+this.dataGymID+'id":'+code+'}'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
</style>
