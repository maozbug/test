<template>
  <div class="hello">
    <div id="html2"></div>
    <input type="button" value="截图" @click="takeScreenshot()">
    <!--<div  style="background-image:url('../assets/logo.png')">-->
  </div>
</template>

<script>
  import html2canvas from 'html2canvas';
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  methods: {
    takeScreenshot() {
      var _this = this;
      html2canvas(document.getElementById("html2")).then(function (canvas) {
        var type='png'
        var imgdata=canvas.toDataURL(type);
        // //2.0 将mime-type改为image/octet-stream,强制让浏览器下载
        var fixtype=function(type){
          type=type.toLocaleLowerCase().replace(/jpg/i,'jpeg');
          var r=type.match(/png|jpeg|bmp|gif/)[0];
          return 'image/'+r;
        };
        imgdata=imgdata.replace(fixtype(type),'image/octet-stream');
        var filename=''+new Date().getDate()+'.'+type;
        _this.savaFile(imgdata,filename);
      });
    },
    savaFile(data,filename) {
      var save_link=document.createElementNS('http://www.w3.org/1999/xhtml', 'a');
      save_link.href=data;
      save_link.download=filename;
      var event=document.createEvent('MouseEvents');
      event.initMouseEvent('click',true,false,window,0,0,0,0,0,false,false,false,false,0,null);
      save_link.dispatchEvent(event);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#html2{
  height: 300px;
  width: 100%;
  background: url("../assets/logo.png") no-repeat;
  background-size: cover;
}
</style>
