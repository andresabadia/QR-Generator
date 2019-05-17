<template>
  <div class="qr">    
    <div class="dont-print">
      <div class="keychain-properties">Keychain Width (cm) <input type="number" step="0.1" v-model="keychainWidth"></div>
      <div class="keychain-properties">Keychain Height (cm) <input type="number" step="0.1" v-model="keychainHeight"></div>
      <!-- <div class="keychain-properties">QR width and height (cm) <input type="number" step="0.1" v-model="qrWidth"></div> -->
      <div class="keychain-properties">QR width and height (px) <input type="number" step="29" v-model="qrWidth"></div>
      <div class="keychain-properties">Select logo <input type="file" accept="image/png" @change="setLogo($event)"></div>
      <div class="keychain-properties">Logo width and height (px) <input type="number" step="1" v-model="logoWidth"></div>
      <div class="keychain-properties">QR and Logo Scale factor <input type="number" step="0.05" max="1" v-model="qrScale"></div>
      <div class="keychain-properties">Margin button (cm) <input type="number" step="0.1" v-model="marginButtom"></div>
      <div class="keychain-properties">Title <input type="text" v-model="title"></div>
      <div class="keychain-properties">Title font size (pt) <input type="number" step="0.5" v-model="titleSize"></div>
      <div class="keychain-properties">Title margin button (cm) <input type="number" step="0.1" v-model="titleMarginBottom"></div>
      <div class="keychain-properties">String font size (pt) <input type="number" step="0.5" v-model="stringSize"></div>
      <div class="keychain-properties">Gym ID <input type="text" v-model="dataGymID"> Data preview: {{data(9999)}}</div>
      <div class="keychain-properties">Data quantity <input type="number" step="1" v-model="dataQuantity" @change="setData()"></div>
      <div class="keychain-properties"><button @click="print()">PRINT</button></div>
      <div class="keychain" :style="'width:' + keychainWidth + 'cm; height:' + keychainHeight + 'cm;'">
        <div :style="'height:'+marginButtom+'cm; width:'+keychainWidth+'cm'"></div>
        <div class="qr-code-container" :style="'transform: scale(' + qrScale + '); margin-bottom:-'+(qrWidth-qrWidth*qrScale)/2+'px'">
          <!-- <img class="qr-code" :style="'width:' + qrWidth + 'cm'" :src="'https://api.qrserver.com/v1/create-qr-code/?size=300x300&data='+data(9999)+'&ecc=H&format=svg'" alt="" title="" /> -->
          <img class="qr-code" :style="'width:' + qrWidth + 'px'" :src="'https://api.qrserver.com/v1/create-qr-code/?size=300x300&data='+data(9999)+'&ecc=H&format=svg'" alt="" title="" />
          <!-- <div class="logo logo-background" :style="'width:' + logoSize + 'cm; height:' + logoSize + 'cm;'"></div> -->
          <div class="logo logo-background" :style="'width:' + logoSize + 'px; height:' + logoSize + 'px;'"></div>
          <!-- <img class="logo" :style="'width:' + logoWidth + 'cm'" alt="Vue logo" :src="logoSrc==''?'logo.png':logoSrc"> -->
          <img class="logo" :style="'width:' + logoWidth + 'px'" alt="Vue logo" :src="logoSrc==''?'logo.png':logoSrc">
        </div>
        <div class="keychain-string" :style="'font-size:' + stringSize + 'pt; margin-bottom:-'+(qrWidth-qrWidth*qrScale)/2+'px;'">ID: 9999</div>
        <div class="keychain-title" :style="'font-size:' + titleSize + 'pt; margin-bottom:' + titleMarginBottom + 'cm'" >{{title}}</div>
      </div>
    </div>
    <div class="print-me">
      <div class="keychain" :style="'width:' + keychainWidth + 'cm; height:' + keychainHeight + 'cm;'" v-for="code in codes" :key="code">
        <div :style="'height:'+marginButtom+'cm; width:'+keychainWidth+'cm'"></div>
        <div class="qr-code-container" :style="'transform: scale(' + qrScale + '); margin-bottom:-'+(qrWidth-qrWidth*qrScale)/2+'px'">
          <!-- <img class="qr-code" :style="'width:' + qrWidth + 'cm'" :src="'https://api.qrserver.com/v1/create-qr-code/?size=300x300&data='+data(code)+'&ecc=H&format=svg'" alt="" title="" /> -->
          <img class="qr-code" :style="'width:' + qrWidth + 'px'" :src="'https://api.qrserver.com/v1/create-qr-code/?size=300x300&data='+data(code)+'&ecc=H&format=svg'" alt="" title="" />
          <!-- <div class="logo logo-background" :style="'width:' + logoSize + 'cm; height:' + logoSize + 'cm;'"></div> -->
          <div class="logo logo-background" :style="'width:' + logoSize + 'px; height:' + logoSize + 'px;'"></div>
          <!-- <img class="logo" :style="'width:' + logoWidth + 'cm'" alt="Vue logo" :src="logoSrc==''?'logo.png':logoSrc"> -->
          <img class="logo" :style="'width:' + logoWidth + 'px'" alt="Vue logo" :src="logoSrc==''?'logo.png':logoSrc">
        </div>
        <div class="keychain-string" :style="'font-size:' + stringSize + 'pt; margin-bottom:-'+(qrWidth-qrWidth*qrScale)/2+'px;'">ID: {{code}}</div>
        <div class="keychain-title" :style="'font-size:' + titleSize + 'pt; margin-bottom:' + titleMarginBottom + 'cm'" >{{title}}</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data(){
    return{
      keychainWidth: 3.8,
      keychainHeight: 8,
      qrWidth:145,
      qrScale:0.9,
      logoSrc: "",
      logoWidth:1,
      marginButtom:0.2,
      title: "Title",
      titleSize:15,
      titleMarginBottom: 0,
      stringSize:10,
      dataGymID:'zz',
      dataQuantity: 5,
      codes:[
        1,2,3,4,5
      ]

    }
  },
  computed:{
    logoSize(){
      this.logoWidth=this.qrWidth*7/29
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
    data(code){
      return '{"obj":"l","'+this.dataGymID+'id":'+code+'}'
    },
    setData(){
      this.codes=[]
      for(let i=0; i<this.dataQuantity; i++){
        this.codes.push(i+1)
      }
    },
    print(){
      window.print()
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.qr{
  text-align: center;
}
.print-me{
  display: block;
  /* display: none; */
}
.keychain-properties{
  text-align: left;
}
.keychain{
  border: 1px solid black;
  border-radius: 10px;
  display: flex;
  flex-direction: column-reverse;
}
.print-me .keychain{
  float: left;
}
.keychain-title{
  font-weight: bold;
}
.qr-code-container{
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
}
.qr-code-container .logo{
  position: absolute;
}
.logo-background{
  background: white;
 }


@media print {
  body{
    margin:0;
  }
  .dont-print{
    display: none;
  }
  .print-me{
    display: block;
  }
  .keychain{
    page-break-inside: avoid;
  }
  .keychain{
    border: unset;
  }
}
</style>
