<template>
  <canvas>
    <slot name="camera"></slot>
    <slot name="scene"></slot>
  </canvas>
</template>

<script>
import { WebGLRenderer } from 'three';
import Vue from 'vue';

export default {
  name: 'webgl-renderer',
  props: {
    canvas: HTMLElement,
    context: WebGLRenderingContext,
    percision: {
      type: String,
      default: 'highp'
    },
    alpha: {
      type: Boolean,
      default: false
    },
    premultipliedAlpha: {
      type: Boolean,
      default: true
    },
    antialias: {
      type: Boolean,
      default: false
    },
    stencil: {
      type: Boolean,
      default: true
    },
    preserveDrawingBuffer: {
      type: Boolean,
      default: false
    },
    depth: {
      type: Boolean,
      default: true
    },
    logarithmicDepthBuffer: {
      type: Boolean,
      default: false
    },
    width: Number,
    height: Number
  },
  data() {
    return {
      camera: null,
      scene: null,
      renderer: null
    }
  },
  methods: {
    render() {
      this.renderer.render(this.scene, this.camera);
    },
    resize() {
      this.renderer.setSize(this.width || window.innerWidth, this.height || window.innerHeight);
    }
  },
  mounted() {
    this.camera = this.$slots.camera[0].componentInstance.camera;
    this.scene = this.$slots.scene[0].componentInstance.scene;
    this.renderer = new WebGLRenderer({
      canvas: this.canvas || this.$el,
      context: this.context,
      percision: this.percision,
      alpha: this.alpha,
      premultipliedAlpha: this.premultipliedAlpha,
      antialias: this.antialias,
      stencil: this.stencil,
      preserveDrawingBuffer: this.premultipliedAlpha,
      depth: this.depth,
      logarithmicDepthBuffer: this.logarithmicDepthBuffer
    });
    window.addEventListener('resize', this.resize, true);
    this.resize();
    this.render();
  }
}
</script>