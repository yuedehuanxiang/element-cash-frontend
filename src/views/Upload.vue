<template>
  <div class="container">
    <h1 class="mbt-15">上传图片到七牛云，上传前显示缩略图</h1>
    <el-upload action="http://upload.qiniup.com/" :data="uploadForm" :before-upload="handleUpload" :on-success="handleSuccess">
      <el-button slot="trigger" size="small" type="primary">选取文件</el-button>
    </el-upload>
    <p class="mbt-15" v-if="imgPreviewArr.length != 0">已上传图片列表</p>
    <img v-for="(img,index) in imgPreviewArr" :key="index" class="img" :style="{'background-image': 'url(' + img + ')'}">
    <ul class="mbt-15">
      <li class="mb-10" v-for="(imgUrl,index) in imgArr" :key="index">
        <a :href="imgUrl" target="_blank"><span>{{"第" + Number.parseInt(index+1) + "张"}}</span>的七牛云图片链接</a>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  data() {
    return {
      imgPreviewArr: [],
      uploadForm: {
        token:
          "mT57HocLAmbigrjdkn6EDQz7DwgbtqGbExgHd3i3:zfxF3FTlnhyrw5uzqVUxuwvUCdI=:eyJzY29wZSI6ImNoZW5zaHVhaTIwMTgiLCJkZWFkbGluZSI6NzIwMDAwMDE1NTAyNzc5ODB9"
      },
      imgArr: []
    };
  },
  methods: {
    handleUpload(file) {
      const reader = new FileReader();

      reader.readAsDataURL(file);

      reader.onloadend = () => {
        this.imgPreviewArr.unshift(reader.result);
      };
    },
    handleSuccess(response) {
      let url = "http://plmygp3nm.bkt.clouddn.com/" + response.hash;
      this.imgArr.unshift(url);
    }
  }
};
</script>
<style scoped>
.img {
  width: 200px;
  height: 200px;
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;
  margin-right: 10px;
}
.container {
  padding: 32px;
}
.mbt-15 {
  margin: 15px 0;
}
.mb-10 {
  margin-bottom: 10px;
}
</style>
