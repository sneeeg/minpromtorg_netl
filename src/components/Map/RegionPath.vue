<template>
  <path
      :index='index'
      :d='paths.path'
      :fill="getPathColor(region)"
      class='state'
      @mouseover='isActive = true'
      @mouseout='hideTooltip'
      @click="setMapFilter(region)"
      @mouseenter="showToolTip(region)"
      style="{position: relative}"
      :class='{ regionActive: isActive}'/>
</template>

<script>
export default {
  props: {
    region: Object,
    index: Number,
    paths: Object
  },
  data() {
    return {
      isActive: false
    };
  },
  methods: {
    getPathColor(region) {
      if(region.id_count <= 5) {
        return '#D5D1FA'
      }
      if(region.id_count > 5) {
        return '#6C60EE'
      }
      if(region.id_count > 20) {
        return '#2E1CE8'
      }
      if(region.id_count > 50) {
        return '#0D0845'
      }
      if(region.id_count > 100) {
        return '#010001'
      }
    },
    setMapFilter (region) {
      console.log(region)
      this.$emit('mapFilterChange', region)
    },
    showToolTip (region) {
      this.$emit('showTool', region)
    },
    hideTooltip() {
      this.$emit('hideTool')
      this.isActive = false
    }
  }
};
</script>

<style lang="sass">
.state
  stroke-width: 1
  stroke: #fff
</style>
