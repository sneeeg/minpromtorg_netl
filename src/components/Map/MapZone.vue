<template>
  <div class="map_zone">
    <div class="map_zone_item"
         v-for="(item, index) in mapZoneColors"
          :key="index"
    >
      <div class="map_zone_item_rectangle" :style="{background: item}"></div>
      <p>70</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "MapZone",
  data:() => ({
    mapZoneColors: ['#010001', '#0D0845', '#2E1CE8', '#6C60EE', '#D5D1FA']
  })
}
</script>

<style lang="sass" scoped>
.map_zone
  position: absolute
  right: 100px
  bottom: 60px
  &_item
    display: flex
    align-items: center
    p
      font-size: 20px
      color: #999
      margin-left: 15px
    &_rectangle
      width: 20px
      height: 50px
</style>