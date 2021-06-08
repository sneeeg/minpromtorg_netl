<template>
  <div>
    <div class="tooltip" v-if="isShowTooltip">
      <p>Регион: {{activeRegion}}</p>
      <p>Кол-во: {{activeRegionValue}}</p>
    </div>
    <svg viewBox="0 0 990 560"  xmlns="http://www.w3.org/2000/svg">
      <g>
        <RegionPath
            v-for="(item, key) in  mapData"
            @showTool="showTooltip"
            @hideTool="hideTooltip"
            @mapFilterChange="mapFilterChange"
            :key=key
            :paths="paths.find(p => p.id === item.region_id)"
            :index="key"
            :region="item"/>
      </g>
    </svg>
  </div>
</template>

<script>
import RegionPath from './RegionPath'
import path_data from './path_data.json'

export default {
  props: {
    mapData: Array
  },
  data: () => ({
    paths: path_data,
    isShowTooltip: false,
    activeRegion: null,
    activeRegionValue: null
  }),
  methods: {
    mapFilterChange(region) {
      this.$emit('mapFilterChange', region)
    },
    showTooltip (region) {
      this.isShowTooltip = true
      this.activeRegion = region.region_name
      this.activeRegionValue = region.id_count
    },
    hideTooltip () {
      this.isShowTooltip = false
    }
  },
  components: {
    RegionPath
  }
};
</script>

<style scoped>
svg {
  width: 100%;
  .state {
    stroke-width: 2;
    stroke: #000;
    -webkit-transition: stroke 0.5s, stroke-width 0.5s;
    -o-transition: stroke 0.5s, stroke-width 0.5s;
    transition: stroke 0.5s, stroke-width 0.5s;
  }
}
svg .state:hover,
.state.active {
  cursor: pointer;
  stroke-width: 1;
  stroke: #000;
}
path {
  opacity: 0.75;
}
.regionActive {
  fill: #2E1CE8;
  opacity: 0.75;
}
p {
  margin: 0 0 10px;
}
.close {
  float: right;
  font-size: 1.5rem;
  font-weight: bold;
  line-height: 1;
  color: #000;
  text-shadow: 0 1px 0 #fff;
  opacity: 0.5;
}
.close:focus,
.close:hover {
  color: #000;
  text-decoration: none;
  cursor: pointer;
  opacity: 0.75;
}
</style>
