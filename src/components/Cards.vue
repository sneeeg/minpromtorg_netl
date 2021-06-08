<template>
  <div class="cards_grid">
    <div class="card">
      <div class="title"><h1>Сертификаты GMP</h1></div>
      <div class="descr"><p>Количество площадок</p></div>
      <div class="count">
        <h1>{{data.gmp_count}}</h1>
      </div>
      <button>
        <span class="material-icons-round">add_circle</span>
      </button>
    </div>
    <div class="card">
      <div class="title"><h1>Локализованное производство</h1></div>
      <div class="descr"><p>Количество площадок</p></div>
      <div class="count">
        <h1>{{data.local_product_count}}</h1>
      </div>
      <button>
        <span class="material-icons-round">add_circle</span>
      </button>
    </div>
    <div class="card">
      <div class="title"><h1>Лицензиаты</h1></div>
      <div class="count">
        <h1>{{data.license_count}}</h1>
      </div>
      <button>
        <span class="material-icons-round">add_circle</span>
      </button>
    </div>
    <div class="card"
    @mouseenter="isCardHover = true">
      <div class="title"><h1>Регионы</h1></div>
      <div class="count">
        <h1>{{data.region_count}}</h1>
      </div>
      <button>
        <span class="material-icons-round">add_circle</span>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Cards",
  props: ['data']
}
</script>

<style lang="sass" scoped>
.cards_grid
  width: 600px
  margin-left: 25px
  display: flex
  flex-wrap: wrap
  justify-content: space-between

.card
  cursor: pointer
  display: flex
  flex-direction: column
  justify-content: space-between
  width: 290px
  height: 180px
  border-radius: 10px
  padding: 15px 25px 25px
  background: #FFF
  transition: 0.2s
  overflow: hidden
  position: relative
  button
    position: absolute
    right: 22px
    bottom: 22px
    span
      font-size: 30px
      color: #000
      transition: 0.2s
  &:hover
    background: #2E1CE8
  &:hover .title h1
    color: #FFF
  &:hover .descr p
    color: #FFF
  &:hover .count h1
    color: #FFF
  &:hover button span
    color: #fff

.title
  h1
    font-size: 20px
    color: #000
    font-weight: 400
    text-align: left
    line-height: 22px

.descr
  p
    margin-top: 5px
    font-size: 14px
    color: #000
    text-align: left

.count
  display: flex
  justify-content: space-between
  align-items: baseline
  margin-top: 30px
  h1
    color: #000
    line-height: 24px
    font-size: 60px
    font-weight: 400

@media screen and (max-width: 1300px)
  .cards_grid
    width: 700px
</style>
