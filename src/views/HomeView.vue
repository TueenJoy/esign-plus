<template>
  <div class="box">
    <vue-esign ref="esign" :width="300" :height="150" :isCrop="isCrop" :lineWidth="lineWidth" :lineColor="lineColor"
      :bgColor.sync="bgColor" />
    <div>
      <button @click="handleReset">清空画板</button>
      <button @click="handleGenerate">生成图片</button>
    </div>
    <img :src="resultImg" alt="">
  </div>
</template>

<script>
import vueEsign from "vue-esign";
export default {
  components: { vueEsign },
  data() {
    return {
      lineWidth: 6,
      lineColor: "#000000",
      bgColor: "",
      resultImg: "",
      isCrop: false,
    };
  },
  mounted() {},
  methods: {
    handleReset() {
      this.$refs.esign.reset();
    },
    handleGenerate() {
      this.$refs.esign
        .generate({ format: "png", quality: 0.8 })
        .then((res) => {
          this.resultImg = res;
        })
        .catch((err) => {
          console.error(err);
          alert("生成图片失败：" + err.message);
        });
    },
  },
};
</script>
<style scoped>
.box {
  width: 300px;
  height: 150px;
  border: 1px solid red;
}
</style>
