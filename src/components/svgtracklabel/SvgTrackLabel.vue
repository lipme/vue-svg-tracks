<template>
  <text
    :x="1"
    :y="computedY"
    :font-size="textFontSize"
    fill="black"
    font-family="monospace"
  >
    <title>{{ label }}</title>
    {{ displayedLabel }}
  </text>
</template>

<script>
export default {
  props: {
    label: { type: String, default: "" },
    y: { type: Number, default: 1 },
    maxWidth: { type: Number, default: 1 },
    textFontSize: { type: Number, default: 15 },
  },
  computed: {
    computedY() {
      return this.y + this.textFontSize;
    },
    displayLabelLength() {
      return this.maxWidth / 10 - (this.textFontSize - 13);
    },
    displayedLabel() {
      if (this.label.length > this.displayLabelLength + 3) {
        let title = "";
        const splitName = this.label.split("");
        splitName.forEach((x) => {
          if (title.length < this.displayLabelLength)
            title = title.concat(String(x));
        });
        title = title.concat("..");
        return title;
      }
      return this.label;
    },
  },
};
</script>
