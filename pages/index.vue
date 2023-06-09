<template>
  <div>
    <div class="main-block">
      <div class="textCenter">
        <el-upload
          drag
          accept=""
          class="upload-demo"
          action="/upload"
          multiple
          :limit="3"
          :before-upload="handleBeforeUpload"
          :on-exceed="handleExceed"
          :on-change="handleChange"
          :on-error="handleError"
          :on-success="handleSuccess"
          :on-progress="handleProcess"
          :show-file-list="false"
          :file-list="fileList">
          <i class="el-icon-upload"></i>
          <div class="el-upload__text">将文件拖到此处，或<em>点击上传</em></div>
          <div slot="tip" class="el-upload__tip textLeft">
            <div>
              <span>1、音乐或歌词上传</span>
            </div>
            <div>
              <span>2、支持的音乐格式：.mp3 .wav</span>
            </div>
            <div>
              <span>3、支持的歌词格式：.lrc</span>
            </div>
            <div>
              <span style="color:#F56C6C;">4、建议的文件名称：歌曲-歌手.音乐格式，例如：难忘今宵-李谷一.mp3</span>
            </div>
          </div>
        </el-upload>
        <div class="textLeft list-block">
          <div class="progress-block" v-for="(item,index) in fileList" :key="index">
            <div>{{item.name}}</div>
            <div style="margin-top: 5px">
              <el-progress :percentage="item.progressPercent" :show-text="false"></el-progress>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      fileList: []
    };
  },
  methods: {
    handleExceed(files, fileList) {
      this.$message.warning(`当前限制选择 10 个文件，本次选择了 ${files.length} 个文件，共选择了 ${files.length + fileList.length} 个文件`);
    },
    handleSuccess(res, files, fileList){
      this.fileList = fileList;
      this.fileList.forEach((item,index)=>{
        item.progressFlag = false;
        if(item.status == 'success'){
          item.successFlag = true;
          item.progressPercent = 100;
        }else{
          item.successFlag = true;
          item.progressPercent = 100;
        }
      })
    },
    handleError(res, file,fileList){
      // let _self = this;
      // this.fileList = fileList;
      // this.fileList.forEach((item,index)=>{
      //   item.progressFlag = false;
      //   item.successFlag = false;
      //   item.progressPercent = 100;
      // });
    },
    handleProcess(event, file, fileList){
      this.fileList = fileList;
      this.fileList.forEach(item=>{
        if (item.percentage == 100) {

        } else {
          item.progressFlag = true
          item.progressPercent = Math.abs(item.percentage.toFixed(0));
        }
      })
    },
    handleChange(file, fileList){

    },
    handleBeforeUpload(file){
      //console.log(file);
    }
  }
}
</script>
