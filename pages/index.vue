<template>
  <v-layout column justify-center align-center>
    <v-flex xs12 sm8 md6>
      <v-btn @click="check">click</v-btn>
      <v-card  max-width="500"  class="mx-auto">
        <v-list rounded>
          <v-subheader>REPORTS</v-subheader>
          <v-list-item-group  color="primary">
            <v-list-item v-for="label in this.label" :key="label.mid">
              <v-list-item-content>
                <v-list-item-title v-text="label.description"></v-list-item-title>
                <v-list-item-subtitle v-text="label.score"></v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>
          </v-list-item-group>
        </v-list>
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
import axios from "axios";
const KEY = "";
const url = "https://vision.googleapis.com/v1/images:annotate?key=";
const api_url = url + KEY;

export default {
  data() {
    return {
      label: []
    };
  },
  methods: {
    check: function() {
      var imageUrl =
        "https://firebasestorage.googleapis.com/v0/b/train-77065.appspot.com/o/1e8df79c-828a-4fb2-b6fd-9771e17771b1?alt=media&token=73cbc8b7-4501-42f5-aace-d904745d53ab";
      var request = {
        requests: [
          {
            image: {
              source: {
                imageUri: imageUrl
              }
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
      axios
        .post(api_url, request)
        .then(response => {
          for (var i = 0;i < response.data.responses[0].labelAnnotations.length;i++) {
            console.log(response.data.responses[0].labelAnnotations[i]);
            this.label.push(response.data.responses[0].labelAnnotations[i]);
          }
        })
        .catch(error => {
          console.log(error.response);
        });
    }
  }
};
</script>
