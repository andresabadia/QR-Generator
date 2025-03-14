<template>
  <div class="qr">
    <div class="dont-print">
      <div class="dont-print-container">
        <div class="properties-container">
          <h1>Edit</h1>
          <div class="keychain-properties">
            Keychain Width (cm)
            <input type="number" step="0.1" v-model="keychainWidth" />
          </div>
          <div class="keychain-properties">
            Keychain Height (cm)
            <input type="number" step="0.1" v-model="keychainHeight" />
          </div>
          <div class="keychain-properties">
            Margin Top (cm)
            <input type="number" step="0.1" v-model="marginButtom" />
          </div>
          <div class="keychain-properties">---</div>
          <!-- <div class="keychain-properties">Select Title Logo <input type="file" accept="image/png" @change="setTitleLogo($event)"></div> -->
          <div class="keychain-properties">
            Logo width and height (px)
            <input type="number" step="1" v-model="titleLogoWidth" />
          </div>
          <div class="keychain-properties">
            Logo gap (cm) <input type="number" step="0.1" v-model="logoGap" />
          </div>
          <!-- <div class="keychain-properties">Title <input type="text" v-model="title"></div> -->
          <!-- <div class="keychain-properties">Title font size (pt) <input type="number" step="0.5" v-model="titleSize"></div> -->
          <!-- <div class="keychain-properties">Title margin button (cm) <input type="number" step="0.1" v-model="titleMarginBottom"></div> -->
          <div class="keychain-properties">
            String font size (pt)
            <input type="number" step="0.5" v-model="stringSize" />
          </div>
          <div class="keychain-properties">---</div>
          <div class="keychain-properties">
            Select logo
            <input type="file" accept="image/png" @change="setLogo($event)" />
          </div>
          <!-- <div class="keychain-properties">
            Logo width and height (px)
            <input type="number" step="1" v-model="logoWidth" />
          </div> -->
          <div class="keychain-properties">
            QR width and height (px)
            <input type="number" step="1" v-model="qrWidth" />
          </div>
          <div class="keychain-properties">
            QR gap (cm)
            <input type="number" step="0.1" v-model="qrGap" />
          </div>
          <div class="keychain-properties">
            QR 2 width and height (px)
            <input type="number" step="1" v-model="qrWidth2" />
          </div>
          <!-- <div class="keychain-properties">QR and Logo Scale factor <input type="number" step="0.05" max="1" v-model="qrScale"></div> -->
          <div class="keychain-properties">---</div>
          <!-- <div class="keychain-properties">Gym ID <input type="text" v-model="dataGymID"> Data preview: {{data(9999)}}</div> -->
          <!-- <div class="keychain-properties">Data from <input type="number" step="1" v-model="dataFrom" @change="setData()"></div>
          <div class="keychain-properties">Custom Data<input type="text" v-model="dataCustom" @change="setData()"></div> -->
          <div class="keychain-properties">
            Sticker Margin X (cm)
            <input type="number" step="0.01" v-model="stickerMarginX" />
          </div>
          <div class="keychain-properties">
            Sticker Margin Y (cm)
            <input type="number" step="0.01" v-model="stickerMarginY" />
          </div>
          <div class="keychain-properties">
            page to page left (cm)
            <input type="number" step="0.01" v-model="paddingLeft" />
          </div>
          <div class="keychain-properties">
            page to page top (cm)
            <input type="number" step="0.01" v-model="paddingTop" />
          </div>
          <div class="keychain-properties">
            Data <textarea v-model="qrCodes" @input="setData()"></textarea>
          </div>
          <!-- <div class="qr-editor-container">          
            <div class="qr-editor">
              <div class="qr-dot" v-for="dot in dots" :key="dot.id" @click="dot.show=!dot.show" :style="dot.show?'background-color:#00000008':'background-color:#999'">{{dot.id}}</div>
            </div>
            <img class="qr-dot-logo" :style="'width:' + 210*(logoWidth/logoSize) + 'px'" :src="logoSrc==''?'logo.png':logoSrc">
          </div> -->
        </div>
        <div class="qr-editor-container">
          <div>
            <h1>Preview</h1>
            <KeyChain
              :keychainWidth="keychainWidth"
              :keychainHeight="keychainHeight"
              :logoGap="logoGap"
              :qrWidth="qrWidth"
              :qrWidth2="qrWidth2"
              :qrGap="qrGap"
              :qrScale="qrScale"
              :logoSrc="logoSrc"
              :logoWidth="logoWidth"
              :titleLogoSrc="titleLogoSrc"
              :titleLogoWidth="titleLogoWidth"
              :titleLogoMarginBottom="titleLogoMarginBottom"
              :dots="dots"
              :marginButtom="marginButtom"
              :title="title"
              :titleSize="titleSize"
              :titleMarginBottom="titleMarginBottom"
              :stringSize="stringSize"
              :dataGymID="dataGymID"
              code="9999_SR_950123"
            >
            </KeyChain>
          </div>
        </div>
      </div>

      <div class="keychain-properties">
        <button @click="print()">PRINT</button> Select Print to PDF and print
        the PDF File
      </div>
      <hr />
      <h1>Print Preview</h1>
    </div>
    <div class="print-me" :style="'padding-left: ' + paddingLeft + 'cm; padding-top: ' + paddingTop + 'cm'">
      <KeyChain
        :style="'margin: ' + stickerMarginX + 'cm ' + stickerMarginY + 'cm'"
        v-for="code in codes"
        :key="code"
        :logoGap="logoGap"
        :keychainWidth="keychainWidth"
        :keychainHeight="keychainHeight"
        :qrWidth="qrWidth"
        :qrWidth2="qrWidth2"
        :qrGap="qrGap"
        :qrScale="qrScale"
        :logoSrc="logoSrc"
        :logoWidth="logoWidth"
        :titleLogoSrc="titleLogoSrc"
        :titleLogoWidth="titleLogoWidth"
        :titleLogoMarginBottom="titleLogoMarginBottom"
        :dots="dots"
        :marginButtom="marginButtom"
        :title="title"
        :titleSize="titleSize"
        :titleMarginBottom="titleMarginBottom"
        :stringSize="stringSize"
        :dataGymID="dataGymID"
        :code="code"
      >
      </KeyChain>
    </div>
  </div>
</template>

<script>
import KeyChain from "./KeyChain.vue";

export default {
  components: {
    KeyChain,
  },
  created() {
    this.createDots();
    this.setData();
  },
  data() {
    return {
      keychainWidth: 1.69,
      keychainHeight: 3.05,
      qrWidth: 30,
      qrGap: 0.3,
      qrWidth2: 50,
      qrScale: 1,
      logoSrc: "",
      titleLogoSrc: "",
      logoWidth: 30,
      titleLogoWidth: 20,
      marginButtom: 0.1,
      titleLogoMarginBottom: 0.2,
      title: "Title",
      titleSize: 15,
      titleMarginBottom: 0,
      stringSize: 5,
      dataGymID: "zz",
      dataQuantity: 5,
      dataFrom: 1,
      dataTo: 5,
      dataCustom: "6,7",
      codes: [],
      dots: [],
      qrCodes: "9999_SR_950123;9998_SR_950123;9997_SR_950123;9996_SR_950123",
      logoGap: 0.1,
      stickerMarginX: 0.1,
      stickerMarginY: 0,
      paddingLeft: 0.5,
      paddingTop: 0.5,
    };
  },
  computed: {
    logoSize() {
      return (this.qrWidth * 7) / 29;
    },
  },
  methods: {
    setLogo(ev) {
      if (ev.target.files && ev.target.files[0]) {
        const file = ev.target.files[0];
        const reader = new FileReader();
        reader.onload = (e) => {
          // console.log('reader', e.target.result)
          this.logoSrc = e.target.result;
        };
        reader.readAsDataURL(file);
      } else {
        this.logoSrc = "";
      }
    },
    setTitleLogo(ev) {
      if (ev.target.files && ev.target.files[0]) {
        const file = ev.target.files[0];
        const reader = new FileReader();
        reader.onload = (e) => {
          // console.log('reader', e.target.result)
          this.titleLogoSrc = e.target.result;
        };
        reader.readAsDataURL(file);
      } else {
        this.titleLogoSrc = "";
      }
    },
    data(code) {
      return '{"obj":"l","' + this.dataGymID + 'id":' + code + "}";
    },
    createDots() {
      for (let i = 0; i < 49; i++) {
        let data = {
          show: true,
          id: i,
        };
        this.dots.push(data);
      }
    },
    setData() {
      this.codes = [];
      this.codes = this.qrCodes.split(";");
    },
    print() {
      window.print();
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
h1 {
  margin: unset;
  text-align: left;
  font-size: 1.2em;
}
.dont-print-container {
  display: flex;
}
.qr-editor-container {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 50px;
}
.qr-editor {
  display: flex;
  flex-wrap: wrap;
  width: 210px;
  height: 210px;
}
.qr-dot-logo {
  position: absolute;
  z-index: -1;
}
.qr-dot {
  width: 30px;
  height: 30px;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
}
.qr {
  text-align: center;
}
.print-me {
  display: block;
  /* display: none; */
}
.keychain-properties {
  text-align: left;
}
.keychain {
  border: 1px solid black;
  border-radius: 10px;
  display: flex;
  flex-direction: column;
  position: relative;
}
.print-me .keychain {
  float: left;
}
.keychain-title {
  font-weight: bold;
}
.qr-code-container {
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
}
.qr-code-container .logo {
  position: absolute;
}
.title-logo {
  margin: auto;
}
.logo-background {
  display: flex;
  flex-wrap: wrap;
}

:root {
  --border-color: lightgrey;
}
.upper-left,
.upper-right,
.bottom-left,
.bottom-right {
  position: absolute;
  height: 0.15cm;
  width: 0.15cm;
  /* background: red; */
  border: unset;
}
.flex-center {
  display: flex;
  align-items: center;
  justify-content: center;
}

@media print {
  body {
    margin: 0;
  }
  .dont-print {
    display: none;
  }
  .print-me {
    display: block;
  }
  .keychain {
    page-break-inside: avoid;
  }
  .keychain {
    border: unset;
  }
  .upper-left {
    top: 0;
    left: 0;
    border-top: 1px solid var(--border-color);
    border-left: 1px solid var(--border-color);
  }
  .upper-right {
    top: 0;
    right: 0;
    border-top: 1px solid var(--border-color);
    border-right: 1px solid var(--border-color);
  }
  .bottom-left {
    bottom: 0;
    left: 0;
    border-bottom: 1px solid var(--border-color);
    border-left: 1px solid var(--border-color);
  }
  .bottom-right {
    bottom: 0;
    right: 0;
    border-bottom: 1px solid var(--border-color);
    border-right: 1px solid var(--border-color);
  }
}
</style>
