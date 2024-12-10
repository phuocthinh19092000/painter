<template>
    <div class="container">
        <div class="canvas-area">
          <vue-drawing-canvas
            ref="VueCanvasDrawing"
            height="600"
            width="1000"
            :lock="false"
            lineJoin="round"
            :image="image"
            :stroke-type="strokeType"
            :fill-shape="fillShape"
            :eraser="eraser"
            :lineWidth="lineWidth"
            :color="color"
            :background-color="backgroundColor"
            :background-image="backgroundImage"
            :styles="{'border': 'solid 4px #BD0F72', 'border-radius': '30px'}"
            @mousemove="getCoordinate($event)"
          />
          <n-icon  class="editable" color="#BD0F72" size="40" @click="eraser=!eraser">
            <Eraser24Filled v-if="eraser"/>
            <Edit24Filled v-else/>
          </n-icon>
          <p class="coordinate">x-axis: <strong>{{ x }}</strong>, y-axis: <strong>{{ y }}</strong></p>
        </div>
        <div class="tools">
          <!-- <div class="button-container">
            <select v-model="line">
              <option v-for="n in 25" :key="'option-' + n" :value="n">{{ n }}</option>
            </select>
            <input type="color" v-model="color">
            <select v-model="strokeType">
              <option value="line">Line</option>
              <option value="dash">Dash</option>
              <option value="circle">Circle</option>
              <option value="square">Square</option>
              <option value="triangle">Triangle</option>
              <option value="half_triangle">Half Triangle</option>
            </select>
            <button type="button" @click.prevent="fillShape = !fillShape">
              <span v-if="fillShape">Fill</span>
              <span v-else>Stroke</span>
            </button>
          </div> -->
          <div class="action">
            <button class="undo" type="button" @click.prevent="$refs.VueCanvasDrawing.undo()">
                <n-icon size="35"><ArrowLeft24Filled/></n-icon>
            </button>
            <button class="redo" type="button" @click.prevent="$refs.VueCanvasDrawing.redo()">
                <n-icon size="35"><ArrowRight24Filled/></n-icon>
            </button>
            <!-- <button class="clear" type="button" @click.prevent="$refs.VueCanvasDrawing.reset()">Clear</button> -->
          </div>
          <!-- <div class="button-container">
            <div style="margin-right: 30px;">
              <p style="margin-bottom: 0">Background Color:</p>
              <input type="color" v-model="backgroundColor">
            </div>
            <div>
              <p style="margin-bottom: 0">Upload Background Image:</p>
              <input type="file" @change="setImage($event)">
            </div>
            <div>
              <p style="margin-bottom: 0">Upload Watermark Image:</p>
              <input type="file" @change="setWatermarkImage($event)">
            </div>
          </div> -->
        </div>
        
        <!-- <div class="output">
          <p>Output:</p>
          <img :src="image" style="border: solid 1px #000000">
        </div> -->
      </div>
  </template>
<script>
import VueDrawingCanvas from "vue-drawing-canvas";
import { Eraser24Filled, Edit24Filled, ArrowLeft24Filled, ArrowRight24Filled } from '@vicons/fluent'
import { NButton, NIcon } from "naive-ui"
export default {
  name: "App",
  components: {
    VueDrawingCanvas,
    NButton,
    NIcon,
    Eraser24Filled,
    Edit24Filled,
    ArrowRight24Filled,
    ArrowLeft24Filled
  },
  data() {
    return {
      x: 0,
      y: 0,
      image: '',
      eraser: false,
      fillShape: false,
      lineWidth: 5,
      color: '#BD0F72',
      strokeType: 'dash',
      backgroundColor: '#FFFFFF',
      backgroundImage: null,
      watermark: null
    }
  },
  methods: {
    async setImage(event) {
      let URL = window.URL;
      this.backgroundImage = URL.createObjectURL(event.target.files[0]);
      await this.$refs.VueCanvasDrawing.redraw();
    },
    async setWatermarkImage(event) {
      let URL = window.URL;
      this.watermark = {
        type: "Image",
        source: URL.createObjectURL(event.target.files[0]),
        x: 0,
        y: 0,
        imageStyle: {
          width: 600,
          height: 400
        }
      }
      await this.$refs.VueCanvasDrawing.redraw();
    },
    getCoordinate(event) {
      let coordinates = this.$refs.VueCanvasDrawing.getCoordinates(event);
      this.x = coordinates.x;
      this.y = coordinates.y;
    }
  }
};

</script>
<style lang="scss" scoped>
.container {
    display: flex;
    flex-direction: column;
    justify-items: center;
    gap: 12px;
    .canvas-area {
        display: flex;
        justify-content: center;
        position: relative;
        cursor: pointer;
        .editable {
            position: absolute;
            top: 10px;
        }
        .coordinate {
            position: absolute;
            bottom: 0;
            padding: 5px 10px;
            background-color: #BD0F72;
            border-radius: 30px;
            color: rgb(230, 230, 230);
            text-align: center;
        }
    }
    .tools {
        display: flex;
        justify-content: center;
        .action {
            width: 100%;
            display: flex;
            justify-content: space-evenly;
            button {
                display: flex;
                justify-content: center;
                align-items: center;
                gap: 10px;
                position: relative;
                padding: 5px 20px;
                background-color: #BD0F72;
                border: solid 1px #BD0F72;
                color: #e7e2e5;
                border-radius: 20px;
                font-size: larger;
                font-weight: 700;
            }
        }
    }
}
</style>
