<template>
  <div class="map">
    <div class="map_header">
      <h1>Всего:</h1>
      <h1>{{totalMapCount}}</h1>
    </div>
    <button class="map_button">
      <span class="material-icons-round">add_circle</span>
    </button>
    <MapChart
        :mapData="mapData"
        :countryData="{'IE': 14, 'ES': 21}"
        highColor="#ff0000"
        lowColor="#aaaaaa"
        countryStrokeColor="#909090"
        defaultCountryFillColor="#dadada"
        @mapFilterChange="mapFilterChange"
    />
    <MapZone />
  </div>
</template>

<script>
import MapChart from './Map/MapChart'
import MapZone from './Map/MapZone'

export default {
name: "Map",
  components: { MapChart, MapZone },
  props: ['mapData', 'totalMapCount'],
  methods: {
    mapFilterChange(region) {
      this.$emit('mapFilterChange', region)
    }
  }
}
</script>

<style lang="sass" scoped>
.map_button 
  position: absolute
  bottom: 24px
  right: 24px
  span
    font-size: 30px

.map
  width: 870px
  height: 380px
  overflow: hidden
  position: relative
  background: #FFF
  border-radius: 10px
  padding: 40px 40px

  &_header
    h1
      font-size: 35px
      font-weight: 400
      line-height: 22px
      color: #000
      &:not(:first-child)
        margin-top: 15px
  &_content
    height: 300px
    img
      width: 100%
      height: 100%
      object-fit: contain
</style>
