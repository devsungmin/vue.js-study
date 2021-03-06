<template>
  <v-navigation-drawer v-model="pallete" clipped app>
    <v-list class="sidebar-list layer" nav rounded elevation expand>
      <v-list-item>
        <v-list-item-content>
          <v-text-field
            v-model="searchlayer"
            placeholder="search"
            prepend-inner-icon="mdi-magnify"
            @input="search"
          />
        </v-list-item-content>
      </v-list-item>

      <v-list-group v-for="layername in layersname" :key="layername.name">
        <template v-slot:activator>
          <v-list-item-title>
            <v-icon style="margin-right: 8%">mdi-layers</v-icon>
            {{ layername.name }}
          </v-list-item-title>
        </template>
        <draggable :list="layers" :group="{ type: 'layer', pull: 'clone' }">
          <v-list-item
            class="layers"
            v-for="layer in layers"
            :key="layer.type"
            :group="{ type: 'type', put: false }"
          >
            <v-list-item-content>
              <v-list-item-title class="block" v-if="layername.key == layer.key">
                {{ layer.type }}
              </v-list-item-title>

              <!-- <v-list-item-title v-else-if="layername.key != layer.key">
                {{ layer.type }}
              </v-list-item-title> -->
            </v-list-item-content>
          </v-list-item>
        </draggable>
      </v-list-group>
    </v-list>
  </v-navigation-drawer>
</template>

<script>
import draggable from "vuedraggable";
export default {
  name: "Pallete",
  components: {
    draggable,
  },
  data() {
    return {
      searchlayer: "",
      layers: [
        { key: "activation", type: "elu", ID: "a0" },
        { key: "activation", type: "leakyReLU", ID: "a1" },
        { key: "activation", type: "prelu", ID: "a2" },
        { key: "activation", type: "reLU", ID: "a3" },
        { key: "activation", type: "softmax", ID: "a4" },
        { key: "activation", type: "thresholdedReLU", ID: "a5" },
        { key: "basic", type: "activation", ID: "b0" },
        { key: "basic", type: "dense", ID: "b1" },
        { key: "basic", type: "dropout", ID: "b2" },
        { key: "basic", type: "embedding", ID: "b3" },
        { key: "basic", type: "flatten", ID: "b4" },
        { key: "basic", type: "permute", ID: "b5" },
        { key: "basic", type: "repeatVector", ID: "b6" },
        { key: "basic", type: "reshape", ID: "b7" },
        { key: "basic", type: "spatialDropout1d", ID: "b8" },
        { key: "convol", type: "conv1d", ID: "c0" },
        { key: "convol", type: "conv2d", ID: "c1" },
        { key: "convol", type: "conv2dTranspose", ID: "c2" },
        { key: "convol", type: "conv3d", ID: "c3" },
        { key: "convol", type: "cropping2D", ID: "c4" },
        { key: "convol", type: "depthwiseConv2d", ID: "c5" },
        { key: "convol", type: "separableConv2d", ID: "c6" },
        { key: "convol", type: "upSampling2d", ID: "c7" },
        { key: "merge", type: "add", ID: "m0" },
        { key: "merge", type: "average", ID: "m1" },
        { key: "merge", type: "concatenate", ID: "m2" },
        { key: "merge", type: "dot", ID: "m3" },
        { key: "merge", type: "maximum", ID: "m4" },
        { key: "merge", type: "minimum", ID: "m5" },
        { key: "merge", type: "multiply", ID: "m6" },
        { key: "nomalization", type: "batchNormalization", ID: "n0" },
        { key: "nomalization", type: "layerNormalization", ID: "n1" },
        { key: "pooling", type: "averagePooling1d", ID: "p0" },
        { key: "pooling", type: "averagePooling2d", ID: "p1" },
        { key: "pooling", type: "averagePooling3d", ID: "p2" },
        { key: "pooling", type: "globalAveragePooling1d", ID: "p3" },
        { key: "pooling", type: "globalAveragePooling2d", ID: "p4" },
        { key: "pooling", type: "globalMaxPooling1d", ID: "p5" },
        { key: "pooling", type: "globalMaxPooling2d", ID: "p6" },
        { key: "pooling", type: "maxPooling1d", ID: "p7" },
        { key: "pooling", type: "maxPooling2d", ID: "p8" },
        { key: "pooling", type: "maxPooling3d", ID: "p9" },
        { key: "recurrent", type: "gru", ID: "r0" },
        { key: "recurrent", type: "gruCell", ID: "r1" },
        { key: "recurrent", type: "lstm", ID: "r2" },
        { key: "recurrent", type: "lstmCell", ID: "r3" },
        { key: "recurrent", type: "rnn", ID: "r4" },
        { key: "recurrent", type: "simpleRNN", ID: "r5" },
        { key: "recurrent", type: "simpleRNNCell", ID: "r6" },
        { key: "recurrent", type: "stackedRNNCells", ID: "r7" },
        { key: "inputs", type: "inputLayer", ID: "i0" },
        { key: "padding", type: "zeroPadding2d", ID: "p0" },
        { key: "noise", type: "alphaDropout", ID: "n0" },
        { key: "noise", type: "gaussianDropout", ID: "n1" },
        { key: "noise", type: "gaussianNoise", ID: "n2" },
        { key: "mask", type: "masking", ID: "m0" },
        
      ],
      layersname: [
        { key: "activation" , name: "Activation"},
        { key: "basic" , name: "Basic"},
        { key: "convol", name: "Convolutional" },
        { key: "merge" , name: "Merge"},
        { key: "nomalization", name: "Nomalization" },
        { key: "pooling", name: "Pooling" },
        { key: "recurrent" , name: "Recurrent"},
        { key: "wrapper" , name: "Wrapper"},
        { key: "classes" , name: "Classes"},
        { key: "inputs" , name: "Inputs"},
        { key: "padding" , name: "Padding"},
        { key: "noise" , name: "Noise"},
        { key: "mask" , name: "Mask"},
        
      ],
      layerCopy: [],
    };
  },
  mounted() {
    this.layerCopy = [...this.layers];
  },
  methods: {
    search: function() {
      if (!this.searchlayer) {
        this.layers = this.layerCopy;
      }
      this.layers = this.layers.filter((layer) => {
        return (
          layer.type.toLowerCase().indexOf(this.searchlayer.toLowerCase()) > -1
        );
      });
    },
  },
};
</script>

<style lang="sass">
h1
  color: black
  text-align: center

#searchbtn
  margin-top: 5%
  align: end

.v-list-item__content
  padding: 2%
  margin-bottom: 2%
  font-size: 16px

.v-list-item,
.v-list--nav .v-list-item:not(:last-child):not(:only-child),
.v-list--rounded .v-list-item:not(:last-child):not(:only-child)
  margin-bottom: 2%

.v-list-group
  margin-bottom: 20px

.block
  width: 50%
  font-size: 100%
  height: auto
  margin-left: 5%

.convol,
.pooling,
.nomalization
  width: auto
  font-size: 10px
</style>
