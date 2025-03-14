<template>
  <div
    class="keychain"
    :style="'width:' + keychainWidth + 'cm; height:' + keychainHeight + 'cm;'"
  >
    <div class="upper-left"></div>
    <div class="upper-right"></div>
    <div class="bottom-left"></div>
    <div class="bottom-right"></div>
    <div
      :style="'height:' + marginButtom + 'cm; width:' + keychainWidth + 'cm'"
    ></div>
    <div class="flex-center" :style="'gap:' + logoGap + 'cm;'">
      <div
        class="qr-code-container"
        :style="
          'transform: scale(' +
            qrScale +
            '); margin-bottom:-' +
            (qrWidth - qrWidth * qrScale) / 2 +
            'px'
        "
      >
        <img
          class="qr-code"
          :style="'width:' + qrWidth + 'px'"
          :src="
            'https://api.qrserver.com/v1/create-qr-code/?size=300x300&data=' +
              data(code) +
              '&ecc=M&format=svg'
          "
          alt=""
          title=""
        />
      </div>
      <img
        :style="'width:' + titleLogoWidth + 'px;'"
        alt="Vue logo"
        :src="logoSrc == '' ? 'logo.png' : logoSrc"
      />
    </div>
    <div
      class="keychain-string oxygen-mono-regular"
      :style="
        'font-size:' +
          stringSize +
          'pt; margin-bottom:-' +
          (qrWidth - qrWidth * qrScale) / 2 +
          'px;'
      "
    >
      {{ data(code) }}
    </div>
    <div
      :style="'height:' + qrGap + 'cm; width:' + keychainWidth + 'cm'"
    ></div>
    <div
      class="qr-code-container"
      :style="
        'transform: scale(' +
          qrScale +
          '); margin-bottom:-' +
          (qrWidth - qrWidth * qrScale) / 2 +
          'px'
      "
    >
      <img
        class="qr-code"
        :style="'width:' + qrWidth2 + 'px'"
        :src="
          'https://api.qrserver.com/v1/create-qr-code/?size=300x300&data=' +
            data(code) +
            '&ecc=M&format=svg'
        "
        alt=""
        title=""
      />
    </div>
    <div
      class="keychain-string oxygen-mono-regular"
      :style="
        'font-size:' +
          stringSize +
          'pt; margin-bottom:-' +
          (qrWidth - qrWidth * qrScale) / 2 +
          'px;'
      "
    >
      {{ data(code) }}
    </div>
  </div>
</template>

<script>
export default {
  props: [
    "keychainWidth",
    "keychainHeight",
    "qrWidth",
    "qrScale",
    "logoSrc",
    "logoWidth",
    "titleLogoSrc",
    "titleLogoWidth",
    "marginButtom",
    "title",
    "titleSize",
    "titleMarginBottom",
    "titleLogoMarginBottom",
    "stringSize",
    "dataGymID",
    "code",
    "dots",
    "logoGap",
    "qrWidth2",
    "qrGap",
  ],
  data() {
    return {};
  },
  computed: {
    logoBGSize() {
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
    dotColor(condition) {
      if (condition) {
        return "white";
      } else {
        return "transparent";
      }
    },
    data(code) {
      return code;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style></style>
