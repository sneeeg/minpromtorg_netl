<template>
  <header>
    <div class="select_menu">
      <div class="select_menu_btn">
        <button @click="isOpenMenu = !isOpenMenu">{{selectedOption}} <img src="@/assets/header_arrow.svg" :style="{transform: isOpenMenu ? 'rotate(180deg)' : '', transition: '0.5s'}" alt=""></button>
      </div>
      <transition name="show">
        <div class="select_menu_list" v-if="isOpenMenu">
          <button disabled>Все</button>
          <button @click="setHeaderFilter('afs', 'Производство АФС')">Производство АФС</button>
          <button @click="setHeaderFilter('sterile_prod', 'Стерильное производств')">Стерильное производство</button>
          <button @click="setHeaderFilter('non_sterile_prod', 'Нестерильное производство')">Нестерильное производство</button>
          <button @click="setHeaderFilter('immun_drugs', 'Иммунобиологические препараты')">Иммунобиологические препараты</button>
          <button @click="setHeaderFilter('blood_drugs', 'Препараты крови')">Препараты крови</button>
          <button @click="setHeaderFilter('potent', 'Сильнодействующие')">Сильнодействующие</button>
          <button @click="setHeaderFilter('toxic', 'Высокотоксичные')">Высокотоксичные</button>
          <button @click="setHeaderFilter('hormones', 'Гормоны')">Гормоны</button>
          <button @click="setHeaderFilter('cytostatics', 'Цитостатики')">Цитостатики</button>
          <button @click="setHeaderFilter('radiopharm', 'Радиофармпрепараты')">Радиофармпрепараты</button>
          <button @click="setHeaderFilter('herbal', 'Растительные препараты')">Растительные препараты</button>
          <button @click="setHeaderFilter('homeopathic', 'Препараты гомеопатические')">Препараты гомеопатические</button>
          <button @click="setHeaderFilter('gas', 'Производство газов')">Производство газов</button>
        </div>
      </transition>
    </div>
    <div class="btns">
      <button :class="{btn_active : activeSwitch === 'product_site_id'}" class="btn_primary" @click="setActiveSwitch('product_site_id')">Площадки</button>
      <button :class="{btn_active : activeSwitch === 'production_id'}" class="btn_primary" @click="setActiveSwitch('production_id')">Компании</button>
      <div class="btn_clean">
        <button @click="setInitialState">
          Очистить
        </button>
        <svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M10 18C5.059 18 1.15 13.497 2.16 8.37997C2.768 5.29897 5.233 2.80997 8.309 2.17497C11.497 1.51697 14.446 2.77397 16.235 4.99997H18.647C16.639 1.54097 12.627 -0.617028 8.206 0.156972C4.177 0.863972 0.920003 4.07997 0.176003 8.10297C-0.996997 14.447 3.865 20 10 20C15.135 20 19.378 16.11 19.937 11.122C20.004 10.526 19.538 9.99997 18.938 9.99997C18.438 9.99997 18.007 10.369 17.953 10.866C17.52 14.871 14.118 18 10 18Z" fill="#949494"/>
          <path d="M20 1.71595V5.99995C20 6.55195 19.552 6.99995 19 6.99995H14.716C14.083 6.99995 13.766 6.23495 14.214 5.78695L18.788 1.21295C19.235 0.764948 20 1.08195 20 1.71595Z" fill="#949494"/>
        </svg>
      </div>
    </div>
  </header>
</template>

<script>
export default {
name: "Header",
  emits: ['handleChange', 'clean', 'headerGroupSwitch'],
  data: () => ({
    inputOption: 'all',
    isOpenMenu: false,
    selectedOption: 'Все',
    activeSwitch: 'product_site_id'
  }),
  methods: {
    setInitialState() {
      this.inputOption = 'all'
      this.selectedOption = 'Все'
      this.activeSwitch = 'product_site_id'
      this.$emit('clean')
    },
    setHeaderFilter(selectOption, optionLabel) {
      this.selectedOption = optionLabel
      this.isOpenMenu = false
      this.$emit('handleChange', selectOption)
    },
    setActiveSwitch(value) {
      this.activeSwitch = value
      this.$emit('headerGroupSwitch', value)
    }
  }
}
</script>

<style lang="sass" scoped>
header
  height: 50px
  display: flex
  margin-top: 15px

select
  border: 1px solid #DADADA
  border-radius: 5px
  padding-left: 20px

.btns
  margin-left: 35px
  display: flex

.btn_primary
  background: #FFF
  color: #8A8A8A
  border-radius: 5px
  border: 1px solid #DADADA
  width: 240px
  height: 100%

.btn_active
  background: #000
  color: #FFF
  border-radius: 5px
  width: 240px
  height: 100%
  transition: 0.2s

.btn_clean
  margin-left: 10px
  display: flex
  color: #8A8A8A
  align-items: center
  svg
    margin-left: 5px

.select_menu
  position: relative
  display: flex
  align-items: center
  &_btn
    width: 320px
    height: 50px
    background: #fff
    border: 1px solid #ececec
    border-radius: 5px
    button
      width: 100%
      height: 100%
      text-align: start
      display: flex
      align-items: center
      justify-content: space-between
      padding: 0 20px
  &_list
    position: absolute
    width: 320px
    height: 180px
    z-index: 1
    overflow: auto
    border-radius: 0 5px 5px 5px
    border: 1px solid #ececec
    box-shadow: 6px 8px 7px -8px rgba(34, 60, 80, 0.2);
    top: 46px
    display: flex
    background: #FFF
    flex-direction: column
    align-items: flex-start
    button
      text-align: start
      width: 100%
      padding: 10px 15px
      transition: 0.2s
      &:hover
        background: #dadada


.show-enter-active, .show-leave-active
  transition: 0.5s ease

.show-enter-from, .show-leave-to
  height: 0
  opacity: 0

</style>
