<template>
  <div class="aside">
    <div class="logo">
      <img src="@/assets/logo.svg" alt="">
    </div>

    <nav>
      <ul>
        <li>
          <button>Российские производители</button>
        </li>
        <li>
          <button>Маркировка</button>
        </li>
        <li>
          <button>GMP проверки</button>
        </li>
        <li>
          <button>Лекарственные препараты</button>
        </li>
      </ul>
    </nav>

    <button class="logout">Выйти</button>
  </div>
</template>

<script>
export default {
name: "Menu"
}
</script>

<style lang="sass" scoped>
.aside
  display: flex
  align-items: center
  flex-direction: column
  width: 345px
  background: #FFF
  padding-top: 10vh

nav
  width: 100%
  margin-top: 50px
  border-bottom: 1px solid #E1E1E2

ul
  padding: 0
  list-style: none
  li
    height: 85px
    display: flex
    align-items: center
    button
      text-align: start
      width: 100%
      height: 100%
      padding: 0 70px
      color: #868686
      font-size: 18px
      transition: 0.2s
      &:hover
        background: #F9F9F9

.logout
  margin-top: 35px
  font-size: 18px
  color: #000000
  text-align: left
  text-decoration: underline
</style>
