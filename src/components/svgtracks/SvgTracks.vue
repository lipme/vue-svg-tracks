<template>
  <g>
    <svg-track
      v-for="(track, index) in tracks"
      :key="'track-' + index"
      :length="length"
      :y="trackY[index]"
      :fct-scale-x="coordX"
      :track="track"
      :text-font-size="fontSize"
      :height="trackHeight"
      :displayLabel="displayLabels"
      :tooltip="tooltip"
    />
  </g>
</template>

<script>
import * as d3 from 'd3-scale'
import SvgTrack from '@/components/svgtrack'

export default {
  components: { SvgTrack },
  name: 'vue-svg-tracks',
  props: {
    tracks: {
      type: Array,
      default: () => []
    },
    length: {
      type: Number,
      default: 100
    },
    trackHeight: {
      type: Number,
      default: 10
    },
    offsetX: {
      type: Number,
      default: 200
    },
    width: {
      type: Number,
      default: 800
    },
    sep: {
      type: Number,
      default: 10
    },
    displayLabels: {
      type: Boolean,
      default: true
    },
    tooltip: { type: Boolean, default: true }
  },
  computed: {
    /**
     * Text font size computed according to the height of the sequence tracks.
     */
    fontSize () {
      return this.trackHeight - 2
    },
    /**
     * Return an array of the coordinate 'y' values
     * of the metadat tracks
     * @return {number}  an array of the coordinate 'y' values.
     */
    trackY () {
      const metadataTrackY = []
      for (let i = 0; i <= this.tracks.length; i++) {
        metadataTrackY.push((this.trackHeight + this.sep) * (i + 1))
      }
      return metadataTrackY
    },
    /**
     * Return a function given the coordinate 'x' values
     * coordX(10) is the X coordinate of the text of the 10th letter of a seq.
     * @return {function}
     */
    coordX () {
      const x = d3
        .scaleLinear()
        .domain([0, this.length])
        .range([this.offsetX, this.width])

      return x
    },
    /**
     * return the width of a nucleotide
     */
    letterWidth () {
      return this.trackHeight - 5
    }
  }
}
</script>

<style>
</style>
