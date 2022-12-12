<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <iframe
      ref="kivicubeScene"
      v-bind="props"
      @load="load"
      @error="error"
      @ready="ready"
      @downloadAssetStart="downloadAssetStart"
      @downloadAssetProgress="downloadAssetProgress"
      @downloadAssetEnd="downloadAssetEnd"
      @loadSceneStart="loadSceneStart"
      @loadSceneEnd="loadSceneEnd"
      @sceneStart="sceneStart"
    ></iframe>
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  },
  data() {
    return {
      props: {},
    };
  },
  async mounted() {
    // 变量kivicubeIframePlugin来自于kivicube lib：https://www.kivicube.com/lib/iframe-plugin.js
    // index.html之中使用script标签引入。
    // eslint-disable-next-line no-undef
    this.props = kivicubeIframePlugin.openKivicubeScene(
      this.$refs.kivicubeScene,
      {
        sceneId: "rDM7kXvo1UJKHnQUR46s7neoCSutDul9",
        hideLogo: true,
        hideTitle: true,
        hideDownload: true,
        hideLoading: true,
        hideScan: true,
        hideTakePhoto: true,
        hideBackground: true,
      },
      false
    );
  },
  beforeDestroy() {
    window.kivicubeIframePlugin.destroyKivicubeScene(
      this.$refs.kivicubeScene
    );
  },
  methods: {
    load() {
      console.log("load");
    },

    error() {
      console.log("error");
    },

    ready({ detail }) {
      console.log("ready", detail);
    },

    downloadAssetStart() {
      console.log("downloadAssetStart");
    },

    downloadAssetProgress({ detail }) {
      console.log("downloadAssetProgress", detail);
    },

    downloadAssetEnd() {
      console.log("downloadAssetEnd");
    },

    loadSceneStart() {
      console.log("loadSceneStart");
    },

    loadSceneEnd() {
      console.log("loadSceneEnd");
    },

    sceneStart() {
      console.log("sceneStart");
    }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
iframe {
  width: 80vw;
  height: calc(80vw * (4 / 3));
  margin: 5vw auto;
  border: none;
}
</style>
