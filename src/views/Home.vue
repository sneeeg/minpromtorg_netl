<template>
  <div class="home">
    <Header @handleChange="headerOptionChange" @headerGroupSwitch="headerGroupSwitch" @clean="headerClean"/>
    <Loader />
    <div class="content_container">
      <section>
        <Map :mapData="mapData" :totalMapCount="totalMapCount" @mapFilterChange="mapFilterChange" v-if="mapData && countData && formsData && sizeData"/>
        <Cards :data="countData" v-if="mapData && countData && formsData && sizeData"/>
      </section>

      <section>
        <Size
            v-if="mapData && countData && formsData && sizeData"
            :data="sizeData"
            :activeSize="activeSizeFilterId"
            @checkSize="updateSizeData"
        />
        <Forms
            :dataSet="formsData"
            :totalValueForms="totalValueForms"
            v-if="mapData && countData && formsData && sizeData"
            @handleChange="formsFilterChange"
        />
      </section>
    </div>
  </div>
</template>

<script>


import Map from "@/components/Map";
import Cards from "@/components/Cards";
import Forms from "@/components/Forms";
import Size from "@/components/Size";
import Header from "@/components/Header";
import Loader from "@/components/Loader";
import axios from 'axios'
export default {
  name: 'Home',
  components: {
    Loader,
    Header,
    Size,
    Forms,
    Cards,
    Map
  },
  data: () => ({
    sizeData: null,
    countData: null,
    formsData: null,
    mapData: null,
    activeSizeFilterId: null,
    totalValueForms: 0,
    totalMapCount: 0,
    filterParams: {
      group_by: 'product_site_id',
      lf_id: undefined,
      region_id: undefined,
      production_size_id: undefined,
    }
  }),
  methods: {
    getInitialState() {
      axios.get('https://api.def.team/api/v1/get_size_data', {params: this.filterParams})
          .then(response => this.sizeData = response.data.answer);
      axios.get('https://api.def.team/api/v1/get_count_data', {params: this.filterParams})
          .then(response => (this.countData = response.data.answer));
      axios.get('https://api.def.team/api/v1/get_lf_data', {params: this.filterParams})
          .then(response => {
            this.formsData = response.data.answer
            this.totalValueForms = 0
            response.data.answer.map(
                (item) => {
                  this.totalValueForms = this.totalValueForms + item.value
                }
            )
          });
      axios.get('https://api.def.team/api/v1/get_map_data', {params: this.filterParams})
          .then(response => {
            this.mapData = response.data.answer
            this.totalMapCount = 0
            response.data.answer.map(
                (item) => {
                  this.totalMapCount = this.totalMapCount + item.id_count
                }
            )
          });
    },

    updateSizeData(id) {
      this.filterParams.production_size_id = id
      this.getInitialState()
    },

    formsFilterChange(id) {
      this.filterParams.lf_id = id
      this.getInitialState()
    },

    headerGroupSwitch(value) {
      this.filterParams.group_by = value
      this.getInitialState()
    },

    headerClean() {
      this.activeSizeFilterId = null
      this.filterParams.production_size_id = undefined
      this.filterParams.region_id = undefined
      this.filterParams.group_by = 'product_site_id'
      this.filterParams.lf_id = undefined
      this.getInitialState()
    },


    headerOptionChange(value) {
      fetch(`https://api.def.team/api/v1/get_size_data?group_by=production_id&${value}=true`).then(
          (resp) => resp.json(). then(
              (data) => {
                this.sizeData = data.answer
              }
          )
      )
      fetch(`https://api.def.team/api/v1/get_count_data?group_by=production_id&${value}=true`).then(
          (resp) => resp.json(). then(
              (data) => {
                this.countData = data.answer
              }
          )
      )
      fetch(`https://api.def.team/api/v1/get_lf_data?group_by=production_id&${value}=true`).then(
          (resp) => resp.json(). then(
              (data) => {
                this.formsData = data.answer
              }
          )
      )
    },

    mapFilterChange(region) {
      this.filterParams.region_id = region.region_id
      this.getInitialState()
    }
  },

  created() {
    this.getInitialState()
  }
}
</script>

<style lang="sass" scoped>
section
  display: flex
  margin-top: 25px

.home
  width: 100%
  height: 100%
  padding: 15px 30px

.content_container
  margin-top: 45px
</style>
