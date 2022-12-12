<template>
  <div id="mainDiv" class="">

    <div class="row">
      <div class="col-md-12">
        <h3>
          QR-Code Generator
        </h3>
      </div>
    </div>

    <div class="row">
      <div class="col-md-3 text-lg-right">
        <label for="url" class="m-2" > <b>Enter The Content:</b></label>
      </div>
      <div class="col-md-7 form-group">
        <input 
            type="text"
            class="form-control"
            id="qr-code-content"
            placeholder="Enter the content to convert qr code"
            v-model="qrvalue"
            >
      </div>
    </div>
    <div class="row">
      <div class="col-md-12" style="align-item:center;">
        <button class="btn btn-success" @click="generateQrCode">
          <div v-if="loadding" class="spinner-border spinner-border-sm"></div>
          Generate QR-Code</button>
      </div>
    </div>


    <div class="row m-t-45" align="center">
      <div class="col-md-12">
        <div class="popup-screen" v-if="generateQrCodeFlag">
          <div class="popup-box">
            <div id="qrCodeGenerator">
              <VueQRCodeComponent 
                :text="qrcode.value"
                :size="qrcode.size"
                :color="qrcode.qrcodeColor"
                :bg-color="qrcode.bgColor"
                :error-level="qrcode.errorLevel"
              ></VueQRCodeComponent>
            </div>
            <div style="margin-top: 20px;">
                <button class="btn btn-outline-primary m-3" @click="printQrCode" >Print QR Code</button>
                <button class="btn btn-outline-secondary m-3" @click="qrCodeSlider" >Close</button>
            </div>
          </div>
        </div>
      </div>
    </div>

  </div>
</template>

<script>

import VueQRCodeComponent from 'vue-qrcode-component';

export default {
  name: 'home-components',
  components: {
    VueQRCodeComponent,
  },
  props: {

  },
  data(){
    return{
      qrvalue:'',
      qrcode: {
        value:'sss',
        size:'200',
        qrcodeColor:'black',
        bgColor:'white',
        errorLevel:'H'
      },
      generateQrCodeFlag: false,
      loadding: false,
    }
  },
  methods:{

    // Function For Creating the qr code
    generateQrCode(){
      const self = this;
      if(self.qrvalue) {
        self.qrcode.value = self.qrvalue;
        self.loadding = !false;
        setTimeout(()=>{
          self.loadding = !true;
          self.generateQrCodeFlag = true;
        },500);
      }
    },

    // Print Qr code Function
    printQrCode(){
      var prtContent = document.getElementById("qrCodeGenerator");
      var WinPrint = window.open(
          "",
          "",
          "letf=0,top=0,width=1,height=1,toolbar=0,scrollbars=0,status=0"
      );
      WinPrint.document.write(prtContent.outerHTML);
      setTimeout(function()
      {
          WinPrint.document.close();
          WinPrint.focus();
          WinPrint.print();
          // WinPrint.close();
      }, 2000);
    },

    // This Function For Open Qr code Slider
    qrCodeSlider(){
      const self = this;
      self.generateQrCodeFlag = false;
    }
  },
  mounted(){

  },
  // watch:{
  //   generateQrCodeFlag(){
  //     if(this.generateQrCodeFlag){
  //       this.qrcode.value='';
  //     }
  //   }
  // }
}

</script>

<style scoped>

h3{
  font-family: sans-serif;
  font-weight: bold;
  color: black;
  text-decoration: underline;
}

div {
  margin-top: 10px;
}

#mainDiv{
  margin-top: 80px;
  text-align: center !important;
}

.popup-screen {
    
    z-index: 9999;
    position:fixed;
    top: 0;
    background: rgba(255, 255, 255, 0.1);
    backdrop-filter: blur(5px);
    width: 100%;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    overflow: hidden;

}

.popup-box{
    position: absolute;
    background: rgba(255, 255, 255, 0.8);
    backdrop-filter: blur(10px);
    /* max-width: 600px; */
    display: block;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    margin: 20px;
    padding: 50px 40px;
    border-radius: 20px;
    box-shadow: 0 5px 25px rgb(0 0 0 / 20%);
    overflow: hidden;
}


</style>