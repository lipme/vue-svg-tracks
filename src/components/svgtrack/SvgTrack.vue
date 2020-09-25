<template>
  <g>
    <svg-track-label
      v-if="displayLabel"
      :y="y"
      :max-width="fctScaleX(0) + 1"
      :label="track.trackLabel"
      :text-font-size="textFontSize"
    ></svg-track-label>
    <svg-track-content
      :length="length"
      :y="y"
      :track="track"
      :a-x="fctScaleX"
      :height="height"
    >
    </svg-track-content>
  </g>
</template>

<script>
import SvgTrackLabel from '@/components/svgtracklabel'
import SvgTrackContent from '@/components/svgtrackcontent'

export default {
  components: {
    SvgTrackLabel,
    SvgTrackContent
  },
  props: {
    track: {
      type: Object,
      default () {
        return {}
      }
    },
    y: { type: Number, default: 1 },
    fctScaleX: { type: Function, default: () => {} },
    length: { type: Number, default: 150 },
    textFontSize: { type: Number, default: 10 },
    height: { type: Number, default: 10 },
    displayLabel: { type: Boolean, default: true }
  }
}
</script>
