<template>
  <div class="hello">
    <color-picker v-bind="color" @input="onInput"></color-picker>
    <div style="margin-top: 20px;">Selected color: {{ selectedColor }}</div>
  </div>
</template>

<script>
import ColorPicker from "@radial-color-picker/vue-color-picker";

export default {
  name: "HelloWorld",
  components: { ColorPicker },
  props: {
    msg: String,
  },
  data() {
    return {
      color: {
        hue: 50,
        saturation: 100,
        luminosity: 50,
        alpha: 1,
      },
      selectedColor: "",
    };
  },
  methods: {
    onInput(hue) {
      console.log(this.color);
      this.color.hue = hue;
      this.selectedColor = this.hslToRgb(
        this.color.hue / 359,
        this.color.saturation / 100,
        this.color.luminosity / 100
      );
    },
    hslToRgb(h, s, l) {
      var r, g, b;

      function hue2rgb(p, q, t) {
        if (t < 0) t += 1;
        if (t > 1) t -= 1;
        if (t < 1 / 6) return p + (q - p) * 6 * t;
        if (t < 1 / 2) return q;
        if (t < 2 / 3) return p + (q - p) * (2 / 3 - t) * 6;
        return p;
      }

      if (s == 0) {
        r = g = b = l; // achromatic
      } else {
        var q = l < 0.5 ? l * (1 + s) : l + s - l * s;
        var p = 2 * l - q;

        r = hue2rgb(p, q, h + 1 / 3);
        g = hue2rgb(p, q, h);
        b = hue2rgb(p, q, h - 1 / 3);
      }

      return [Math.floor(r * 255), Math.floor(g * 255), Math.floor(b * 255)];
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import "~@radial-color-picker/vue-color-picker/dist/vue-color-picker.min.css";

h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
