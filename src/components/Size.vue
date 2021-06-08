<template>
  <div class="size">
    <div class="size_content">
      <div class="text_block">
        <div class="text_block_header">
          <h1>Размер</h1>
          <p>Количество площадок</p>
        </div>
        <div class="text_block_content">
          <div
              v-for="size in data"
              :key="size.production_size_id"
              class="size_item"
              :class="{size_active: activeSize === size.production_size_id}"
              @click="$emit('checkSize', size.production_size_id)"
          >
            <div class="flex_row">
              <div class="size_item_color" :style="{background: size.color}"></div>
              <p>{{size.production_size_name}}</p>
            </div>
            <h1>{{size.id_count}}</h1>
          </div>
        </div>
      </div>
      <div class="graph_wrapper">
        <div class="graph">
          <DoghnutChart :data=data />
        </div>
      </div>
    </div>
    <button class="plus_btn">
      <span class="material-icons-round">add_circle</span>
    </button>
  </div>
</template>

<script>
import DoghnutChart from "./DoghnutChart";

export default {
  name: "Size",
  components: {
    DoghnutChart
  },
  props: ['data', 'activeSize'],
  emits: ['checkSize']
}
</script>

<style lang="sass" scoped>
.size
  width: 870px
  height: 420px
  background: #FFF
  border-radius: 10px
  padding: 28px 0px 28px 40px
  overflow: hidden
  position: relative
  &_content
    display: flex
    justify-content: space-between
  &_item
    cursor: pointer
    display: flex
    align-items: center
    justify-content: space-between
    &:hover p
      color: #4d00ca
    &:not(:first-child)
      margin-top: 18px
    p
      font-size: 18px
      color: #868686
      transition: 0.2s
      margin-left: 10px
    h1
      font-size: 30px
      font-weight: 400
      color: #000
    &_color
      background: #e9e9e9
      width: 20px
      height: 20px
      border-radius: 3px

.size_active
  p
    color: #4d00ca

.text_block
  width: 50%
  padding-right: 50px
  border-right: 1px solid #E1E1E2
  &_header
    h1
      font-size: 35px
      font-weight: 400
      color: #000
    p
      font-size: 20px
      margin-top: 10px
  &_content
    margin-top: 46px

.graph
  width: 100%
  &_wrapper
    display: flex
    align-items: center
    justify-content: center

.plus_btn
  position: absolute
  right: 24px
  bottom: 24px
  span
    font-size: 30px
</style>
