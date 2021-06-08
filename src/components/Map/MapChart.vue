<template>
  <div class="wrapper" @click="goEvent($event)">
    <RussianMap @mapFilterChange="mapFilterChange" :mapData="mapData"/>
<!--    <v-dialog/>-->
<!--    <PulseMarker v-if="x && y" :pointX="x" :pointY="y"/>-->
  </div>
</template>

<script>
import RussianMap from "./RussianMap";
// import PulseMarker from "./PulseMarker";
export default {
  props: {
    msg: String,
    mapData: Array
  },
  data: () => ({
    x: null,
    y: null
  }),
  methods: {
    mapFilterChange(region) {
      this.$emit('mapFilterChange', region)
    },
    goEvent(event) {
      this.x = event.x - 25;
      this.y = event.y - 25;
    }
  },
  components: {
    RussianMap,
    // PulseMarker
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="sass">
*
  margin: 0
  padding: 0

.wrapper
  position: absolute
  left: 100px
  top: 15px
  margin: 0 auto
  width: 580px

.tooltip
  position: absolute
  left: 300px
  max-width: 200px
  top: 50px
  background: rgba(0,0,0,0.5)
  border-radius: 5px
  p
    font-size: 14px
    padding: 10px 5px
    color: #fff
    margin: 0
</style>
