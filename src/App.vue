<template>
  <div id="app">
    <div class="container">
      <div class="row">
        <div class="col-md-3">
          <div class="thumbnail">

            <img id="bear" alt="Vue logo" class="img-rounded" src="./assets/teddybear.jpg">

            <div class="caption">
              <h1 v-if="this.predictions !== undefined && this.predictions.filter(p => p.id === 'bear')[0] !== undefined" >
                {{this.predictions.filter(p => p.id === 'bear')[0].result.class}}
              </h1>
              <button  type="button" class="btn btn-light" v-on:click="recogObject('bear')">
                predict
              </button>
            </div>

          </div>
        </div>
        <div class="col-md-3">
          <div class="thumbnail">
            <img id="cat" class="img-rounded" alt="Vue logo" src="./assets/cat.jpg">
            <div class="caption">
            <h1 v-if="this.predictions !== undefined && this.predictions.filter(p => p.id === 'cat')[0] !== undefined" >
              {{this.predictions.filter(p => p.id === 'cat')[0].result.class}}
            </h1>
            <button  type="button" class="btn btn-light" v-on:click="recogObject('cat')">
              predict
            </button>
            </div>
          </div>
        </div>
        <div class="col-md-3">
          <div class="thumbnail">

            <img id="eagle" alt="Vue logo" class="img-rounded" src="./assets/eagle.jpg">

            <div class="caption">
              <h1 v-if="this.predictions !== undefined && this.predictions.filter(p => p.id === 'eagle')[0] !== undefined" >
                {{this.predictions.filter(p => p.id === 'eagle')[0].result.class}}
              </h1>
              <button  type="button" class="btn btn-light" v-on:click="recogObject('eagle')">
                predict
              </button>
            </div>

          </div>
        </div>
        <div class="col-md-3">
          <div class="thumbnail">

            <img id="shark" alt="Vue logo" class="img-rounded" src="./assets/shark.png">

            <div class="caption">
              <h1 v-if="this.predictions !== undefined && this.predictions.filter(p => p.id === 'shark')[0] !== undefined" >
                {{this.predictions.filter(p => p.id === 'shark')[0].result.class}}
              </h1>
              <button  type="button" class="btn btn-light" v-on:click="recogObject('shark')">
                predict
              </button>
            </div>

          </div>
        </div>
      </div>
      <div class="row">
        <div class="col-md-3">
          <div class="thumbnail">

            <img id="scott" alt="Vue logo" class="img-rounded" src="./assets/scott.jpg">

            <div class="caption">
              <h1 v-if="this.predictions !== undefined && this.predictions.filter(p => p.id === 'scott')[0] !== undefined" >
                {{this.predictions.filter(p => p.id === 'scott')[0].result.class}}
              </h1>
              <button  type="button" class="btn btn-light" v-on:click="recogObject('scott')">
                predict
              </button>
            </div>

          </div>
        </div>
        <div class="col-md-3">
          <div class="thumbnail">

            <img id="omer" alt="Vue logo" class="img-rounded" src="./assets/omer.jpg">

            <div class="caption">
              <h1 v-if="this.predictions !== undefined && this.predictions.filter(p => p.id === 'omer')[0] !== undefined" >
                {{this.predictions.filter(p => p.id === 'omer')[0].result.class}}
              </h1>
              <button  type="button" class="btn btn-light" v-on:click="recogObject('omer')">
                predict
              </button>
            </div>

          </div>
        </div>
      </div>      
    </div>
  </div>
</template>

<script>
import * as cocoSsd from '@tensorflow-models/coco-ssd'
let modelPromise;

export default {
  name: 'app',
  data: function () {
    return {
      predictions: []

    }
  },
  async mounted() {
    // Load the model.
    modelPromise = await cocoSsd.load();
    console.log("model loaded")
  },
  methods: {
    async recogObject(id) {
      const img = document.getElementById(id);
    
      // Classify the image.
      const predictions = await modelPromise.detect(img);
      console.log(predictions)
      this.predictions.push({id:id, result: predictions[0]})
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
