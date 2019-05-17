<template>
  <div class="qr">    
    <div class="dont-print">
      <div class="dont-print-container">
        <div class="properties-container">
          <h1>Edit</h1>
          <div class="keychain-properties">Keychain Width (cm) <input type="number" step="0.1" v-model="keychainWidth"></div>
          <div class="keychain-properties">Keychain Height (cm) <input type="number" step="0.1" v-model="keychainHeight"></div>
          <div class="keychain-properties">Margin button (cm) <input type="number" step="0.1" v-model="marginButtom"></div>
          <div class="keychain-properties">---</div>
          <div class="keychain-properties">Select logo <input type="file" accept="image/png" @change="setLogo($event)"></div>
          <div class="keychain-properties">Logo width and height (px) <input type="number" step="1" v-model="logoWidth"></div>
          <div class="keychain-properties">QR width and height (px) <input type="number" step="29" v-model="qrWidth"></div>
          <div class="keychain-properties">QR and Logo Scale factor <input type="number" step="0.05" max="1" v-model="qrScale"></div>
          <div class="keychain-properties">---</div>
          <div class="keychain-properties">Title <input type="text" v-model="title"></div>
          <div class="keychain-properties">Title font size (pt) <input type="number" step="0.5" v-model="titleSize"></div>
          <div class="keychain-properties">Title margin button (cm) <input type="number" step="0.1" v-model="titleMarginBottom"></div>
          <div class="keychain-properties">String font size (pt) <input type="number" step="0.5" v-model="stringSize"></div>
          <div class="keychain-properties">---</div>
          <div class="keychain-properties">Gym ID <input type="text" v-model="dataGymID"> Data preview: {{data(9999)}}</div>
          <div class="keychain-properties">Data quantity <input type="number" step="1" v-model="dataQuantity" @change="setData()"></div>
        </div>
        <div class="qr-editor-container">          
          <div class="qr-editor">
            <div class="qr-dot" v-for="dot in dots" :key="dot.id" @click="dot.show=!dot.show" :style="dot.show?'background-color:#00000008':'background-color:#999'">{{dot.id}}</div>
          </div>
          <img class="qr-dot-logo" :style="'width:' + logoWidth*6 + 'px'" :src="logoSrc==''?'logo.png':logoSrc">
        </div>
        <div>
          <h1>Preview</h1>
          <KeyChain
            :keychainWidth="keychainWidth"
            :keychainHeight="keychainHeight"
            :qrWidth="qrWidth"
            :qrScale="qrScale"
            :logoSrc="logoSrc"
            :logoWidth="logoWidth"
            :dots="dots"
            :marginButtom="marginButtom"
            :title="title"
            :titleSize="titleSize"
            :titleMarginBottom="titleMarginBottom"
            :stringSize="stringSize"
            :dataGymID="dataGymID"
            :code="9999">
          </KeyChain>
        </div>
      </div>
      
      <div class="keychain-properties"><button @click="print()">PRINT</button> Select Print to PDF and print the PDF File</div>
      <hr>
      <h1>Print Preview</h1>
    </div>
    <div class="print-me">
      <KeyChain v-for="code in codes" :key="code"
        :keychainWidth="keychainWidth"
        :keychainHeight="keychainHeight"
        :qrWidth="qrWidth"
        :qrScale="qrScale"
        :logoSrc="logoSrc"
        :logoWidth="logoWidth"
        :dots="dots"
        :marginButtom="marginButtom"
        :title="title"
        :titleSize="titleSize"
        :titleMarginBottom="titleMarginBottom"
        :stringSize="stringSize"
        :dataGymID="dataGymID"
        :code="code">
      </KeyChain>
    </div>
  </div>
</template>

<script>
import KeyChain from './KeyChain.vue'

export default {
  components: {
    KeyChain
  },
  created(){
    this.createDots()
  },
  data(){
    return{
      keychainWidth: 3.8,
      keychainHeight: 8,
      qrWidth:145,
      qrScale:0.9,
      logoSrc: "",
      logoWidth:30,
      marginButtom:0.2,
      title: "Title",
      titleSize:15,
      titleMarginBottom: 0,
      stringSize:10,
      dataGymID:'zz',
      dataQuantity: 5,
      codes:[
        1,2,3,4,5
      ],
      dots:[]

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
    createDots(){
      for(let i=0; i<49;i++){
        let data = {
          show:true,
          id:i
          }
        this.dots.push(data)
      }
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
h1{
  margin: unset;
  text-align: left;
  font-size:1.2em;
}
.dont-print-container{
  display: flex;
}
.qr-editor-container{
  position: relative;  
  display: flex;
  align-items: center;
  justify-content: center;
  margin:0 50px;
}
.qr-editor{
  display: flex;
  flex-wrap: wrap;
  width: 210px;
  height: 210px;
}
.qr-dot-logo{
  position: absolute;
  z-index:-1;
}
.qr-dot{  
  width: 30px;
  height: 30px;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
}
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
  display: flex;
  flex-wrap: wrap;
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
