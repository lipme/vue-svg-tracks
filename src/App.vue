<template>
  <div id="app">
    <h1>vue-svg-track</h1>
    <svg :width="width" :height="height">
      <svg-tracks
        :tracks="tracks"
        :length="length"
        :track-height="trackHeight"
        :sep="sep"
        :offset-x="offsetX"
        :display-labels="displayLabels"
        :tooltip="tooltip"
      />
    </svg>
  </div>
</template>

<script>
import SvgTracks from "@/components/svgtracks";

export default {
  name: "App",
  components: {
    SvgTracks,
  },
  data() {
    return {
      width: 700,
      height: 600,
      length: 300,
      trackHeight: 20,
      sep: 5,
      offsetX: 120,
      displayLabels: true,
      tooltip: true,
      tracks: [
        {
          features: [
            {
              positions: [
                [1, 20],
                [109, 234],
              ],
              type: "label1",
              color: "green",
              "fill-opacity": 0.2,
            },
            {
              positions: [[21, 108]],
              type: "label2",
              color: "pink",
            },
          ],
          trackLabel: "track1",
        },
        {
          features: [
            {
              positions: [
                [1, 15],
                [109, 234],
              ],
              type: "label1",
              color: "yellow",
            },
            {
              positions: [
                [50, 65],
                [16, 20],
              ],
              type: "label2",
              color: "red",
            },
          ],
          trackLabel: "track2-test-long-name",
        },
      ],
    };
  },
};
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
</style>
