<template>
  <g>
    <rect
      v-for="(r, index) in getRect"
      :key="index"
      :x="r.x"
      :y="rectY"
      :height="height"
      :width="r.width"
      :style="r.style"
    >
      <title v-if="tooltip">{{ r.title }}</title>
    </rect>
  </g>
</template>

<script>
export default {
  props: {
    track: {
      type: Object,
      default() {
        return {};
      },
    },
    aX: { type: Function, default: () => {} },
    height: { type: Number, default: 8 },
    y: { type: Number, default: 1 },
    length: { type: Number, default: 150 },
    tooltip: { type: Boolean, default: true },
  },
  computed: {
    rectY() {
      return this.y;
    },

    getShift() {
      return Math.round(((this.aX(1) - this.aX(0)) / 2) * 10) / 10;
    },
    /**
     * Build an array of objects with attributes x,color, width
     */
    getRect() {
      const displayedRect = [];
      this.track.features.forEach((f) => {
        if ("positions" in f) {
          f.positions.forEach((pos) => {
            if (typeof pos !== "undefined" && pos.length === 2) {
              displayedRect.push({
                title:
                  this.track.trackLabel +
                  "-" +
                  f.type +
                  "(" +
                  pos[0] +
                  ":" +
                  pos[1] +
                  ")",
                x: this.rectX(pos[0] - 1),
                color: f.color,
                style: this.getStyle(f.color, f["fill-opacity"]),
                width: this.rectX(pos[1]) - this.rectX(pos[0] - 1),
              });
            }
          });
        }
      });
      return displayedRect;
    },
  },
  methods: {
    /** x coordinate of the rectangle at the index i */
    rectX(i) {
      return this.aX(i) - this.getShift;
    },
    getStyle(f, o) {
      var o_style = {};
      o_style["fill"] = f;
      o_style["fill-opacity"] = o;
      return o_style;
    },
  },
};
</script>
