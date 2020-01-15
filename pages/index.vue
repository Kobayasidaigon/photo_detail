<template>
  <v-layout column justify-center align-center>
    <v-flex xs12 sm8 md6>
      <div id="upload_prev" class="upload"></div>
      <label class="upload-img-btn">
        画像を選択
        <input type="file" id="hoge" @change="photo" style="display:none;" />
      </label>
    </v-flex>
    <v-btn @click="check" v-bind:disabled="click">click</v-btn>
    <v-flex xs12 sm8 md6>
      <v-card max-width="500" class="mx-auto">
        <v-list rounded>
          <v-subheader>REPORTS</v-subheader>
          <v-list-item-group color="primary">
            <v-list-item v-for="label in this.label" :key="label.mid">
              <v-list-item-content>
                <v-list-item-title v-text="label.description"></v-list-item-title>
                <v-list-item-subtitle v-text="label.score"></v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>
          </v-list-item-group>
        </v-list>
      </v-card>
      <Chart :label="label" v-if="loaded"></Chart>
    </v-flex>
  </v-layout>
</template>

<script>

import Chart from "~/components/Vuechart.vue"
import axios from "axios";
const KEY = "AIzaSyCVOiQfzqwYai-ecVlvAhlRyG_BS61pKas";
const url = "https://vision.googleapis.com/v1/images:annotate?key=";
const api_url = url + KEY;

export default {
  data() {
    return {
      label: [],
      local_photo: "",
      click:true,
      loaded:false
    };
  },
  methods: {
    async check() {
      var request = {
        requests: [
          {
            image: {
              content: this.local_photo
            },
            features: [
              {
                type: "LABEL_DETECTION",
                maxResults: 5
              }
            ]
          }
        ]
      };
      await  axios.post(api_url, request).then(response => {
          for (var i = 0;i < response.data.responses[0].labelAnnotations.length;i++) {
            this.label.push(response.data.responses[0].labelAnnotations[i]);
          }
        })
        .catch(error => {
          console.log(error.response);
        });
        this.loaded=!this.loaded;
    },
    photo: function(element) {
      var element = document.getElementById("hoge");
      var file = element.files[0];
      var fileReader = new FileReader();
      const self = this
      fileReader.onload = function(element) {
        const img = document.getElementById("upload_prev");
        img.style.backgroundImage = "url(" + element.target.result + ")";

        //base64の値取得
        var damy_photo_url = this.result
        //いらない記述を削除
        self.local_photo = damy_photo_url.slice(23);
        
      };
      fileReader.readAsDataURL(file);
      this.click=!this.click;
    }
  },
  components:{
    Chart
  }
};
</script>

<style scoped>
.upload {
  width: 330px;
  height: 200px;
  margin-top: 32px;
  border-radius: 8px;
  background: transparent;
  background-size: contain;
  background-repeat: no-repeat;
  border: 2px dashed rgba(112, 112, 112, 0.6);
}
.upload > .upload-img-btn {
  display: block;
  max-width: 120px;
  margin: 45% auto;
  padding: 15px;
  text-align: center;
  color: #515151;
  border-radius: 4px;
}
</style>