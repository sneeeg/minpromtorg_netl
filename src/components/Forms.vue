<template>
  <div class="forms">
    <div class="forms_content">
      <div class="text_block">
        <div class="title"><h1>Лекарственные формы</h1></div>
        <div class="list">
          <div class="labels">
            <button @click="setFormFilter(1)">Субстанции</button>
            <button @click="setFormFilter(4)">Жидкие</button>
            <button @click="setFormFilter(5)">Мягкие</button>
            <button @click="setFormFilter(7)">Другие</button>
            <button @click="setFormFilter(3)">Твердые</button>
            <button @click="setFormFilter(6)">Газы медицинские</button>
            <button @click="setFormFilter(2)">Пиявки</button>
          </div>
          <div class="lines" v-if="totalValueForms !== 0">
            <div
                v-for="form in dataSet"
                :key="form.label"
                class="bar_line"
                :style="{width: form.value*100/totalValueForms + '%'}"></div>
          </div>
          <div class="values">
            <p v-for="form in dataSet"
               :key="form.label" >
              {{form.value}}
            </p>
          </div>
        </div>
      </div>
    </div>
    <button class="plus_btn">
      <span class="material-icons-round">add_circle</span>
    </button>
  </div>
</template>

<script>
// import RadarChart from "./RadarChart";
export default {
name: "Forms",
  components: {},
  props: ['dataSet', 'totalValueForms'],
  emits: ['handleChange'],
  data: () => ({
    labels: [],
    values: []
  }),
  methods: {
    setFormFilter(id){
      this.$emit('handleChange', id)
    }
  }
}
</script>

<style lang="sass" scoped>
.forms
  margin-left: 25px
  width: 600px
  background: #FFF
  border-radius: 10px
  padding: 20px 40px
  overflow: hidden
  position: relative
  &_content
    display: flex
    align-items: center
    justify-content: space-between

.text_block
  width: 100%

.form_item
  display: flex
  align-items: center
.bar_line
  height: 20px
  max-width: 100% !important
  background: #2E1CE8
  transition: 0.3s
  &:not(:first-child)
    margin-top: 15px

.title
  h1
    font-size: 35px
    font-weight: 400
    color: #000

.list
  display: flex
  margin-top: 35px
  .labels
    display: flex
    flex-direction: column
    align-items: start
    button
      height: 20px
      font-size: 18px
      transition: 0.2s
      &:not(:first-child)
        margin-top: 15px
      &:hover
        color: #2E1CE8
  .lines
    width: 300px
    margin-left: 10px
  .values
    margin-left: 5px
    p
      height: 20px
      font-size: 20px
      &:not(:first-child)
        margin-top: 15px


.graph
  width: 230px
  &_wrapper
    width: 50%
    display: flex
    align-items: center
    justify-content: center
  img
    width: 100%
    height: 100%
    object-fit: contain

.plus_btn
  position: absolute
  right: 24px
  bottom: 24px
  span
    font-size: 30px
</style>
