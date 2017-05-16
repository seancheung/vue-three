<template>
  <webgl-renderer>
    <perspective-camera slot="camera"></perspective-camera>
    <scene slot="scene" :objects="objects"></scene>
  </webgl-renderer>
</template>

<script>
import Three from './src';
import { BoxGeometry, MeshBasicMaterial, Mesh } from 'three';

export default {
  name: 'app',
  components: {
    'webgl-renderer': Three.WebGLRenderer,
    'perspective-camera': Three.PerspectiveCamera,
    'scene': Three.Scene
  },
  data() {
    return {
      objects: []
    }
  },
  created() {
    const geometry = new BoxGeometry(1, 1, 1);
    const material = new MeshBasicMaterial({ color: 0x00ff00 });
    const cube = new Mesh(geometry, material);
    this.objects.push(cube);
  }
}
</script>
