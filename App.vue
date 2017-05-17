<template>
  <webgl-renderer ref="renderer" :width="width" :height="height" @update="update">
    <perspective-camera slot="camera" :aspect="aspect" :fov="50" :near="0.1" :far="10000" :position="position" :rotation="rotation"></perspective-camera>
    <scene slot="scene">
      <mesh ref="cube" slot="object">
        <box-geometry slot="geometry" :width="1" :height="1" :depth="1"></box-geometry>
        <mesh-basic-material slot="material" :color="color"></mesh-basic-material>
      </mesh>
    </scene>
  </webgl-renderer>
</template>

<script>
import Three from './src';
import { Color, Vector3 } from 'three';

export default {
  name: 'app',
  components: Three,
  data() {
    return {
      width: 0,
      height: 0,
      position: new Vector3(0, 0, 5),
      rotation: new Vector3(30, 0, 0),
      color: new Color(1, 0.5, 0)
    }
  },
  computed: {
    aspect() {
      return this.height ? this.width / this.height : 0;
    }
  },
  methods: {
    animate() {
      requestAnimationFrame(this.animate);
      this.$refs.renderer.render();
    },
    update() {
      this.$refs.cube.object.rotation.x += 0.1;
      this.$refs.cube.object.rotation.y += 0.1;
    },
    setSize() {
      this.width = window.innerWidth;
      this.height = window.innerHeight;
    }
  },
  mounted() {
    window.addEventListener('resize', this.setSize, true);
    this.setSize();
    this.animate();
  }
}
</script>
