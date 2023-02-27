<script lang="jsx" setup>
import { getCurrentInstance /*, ref, withModifiers */ } from 'vue'
import MainView from '@/components/MainView'

// import HelloWorld from './components/HelloWorld.vue'
// import logo from './assets/logo.png'

// const count = ref(0)
/* const inc = () => {
  count.value++
} */

//** @type {(event: Event, ...args: unknown[]) => any} */
// const onClick = withModifiers(inc, ['self'])

const _self = getCurrentInstance()

_self.render = () => <MainView />

/* inst.render = () => (
  <>
    <img { ...{ src: logo } } alt="Vue logo" />
    <button onClick={onClick}>{count.value}</button>
    <HelloWorld msg="Welcome to Vue.js App" />
  </>
) */
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=Roboto+Mono&display=swap');

$primary-color: #14868c;

$sm-radius: 8px;
$md-radius: 16px;
$sm-box: 70px;
$md-box: 90px;
$lg-box: 110px;
$wrapper: 800px;

@mixin boxSize($size) {
  width: $size;
  height: $size;
  display: flex;
  justify-content: center;
  align-items: center;
}

body {
  font-family: 'Roboto Mono', monospace;
  background-color: #f9f9f9;
  overflow-x: hidden;
  overflow-y: auto;
  h1 {
    color: $primary-color;
    text-shadow: 2px 2px 5px rgba(0,0,0,.3);
  }
  h3 {
    margin-bottom: .8rem;
  }
  .radioBox {
    display: flex;
    flex-wrap: wrap;
    input[type=radio] {
      display: none;
    }
    label {
      display: inline-block;
      padding: 4px 12px;
      margin-right: 4px;
      white-space: nowrap;
      color: $primary-color;
      border: 1px solid $primary-color;
      border-radius: $md-radius;
      transition: all .3s;
      cursor: pointer;
      &:first-child {
        font-weight: bold;
      }
      &.checked {
        color: #fff;
        background-color: $primary-color;
      }
    }
  }
  .radioTitle {
    min-width: 120px;
    margin-right: 6px;
  }
  .boxWrapper {
    box-shadow: 0 0 15px rgba(#000, .35);
    padding: 16px;
    max-width: $wrapper;
    min-height: 350px;
    margin: 12px auto;
    &.align-content-stretch, &.align-items-stretch {
      .boxItem {
        height: auto;
      }
    }
  }
  .boxItem {
    @include boxSize($md-box);
    margin: 6px;
    font-size: 20px;
    text-align: center;
    &:nth-child(5n-4) {
      background-color: indianred;
    }
    &:nth-child(5n-3) {
      background-color: darkorange;
      @include boxSize($sm-box);
    }
    &:nth-child(5n-2) {
      background-color: gold;
    }
    &:nth-child(5n-1) {
      background-color: seagreen;
      @include boxSize($lg-box);
    }
    &:nth-child(5n) {
      background-color: steelblue;
    }
  }
  .numberBox {
    display: flex;
    align-items: center;
    .number {
      width: 60px;
      text-align: center;
    }
  }
  .roundBtn {
    border-radius: 50%;
    color: #fff;
    font-size: 20px;
    user-select: none;
    cursor: pointer;
    @include boxSize(24px);
    &.minusBtn {
      background-color: indianred;
    }
    &.plusBtn {
      background-color: seagreen;
    }
  }
  .selectorWrapper {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
  }
  .selector {
    border: 1px solid $primary-color;
    border-radius: $sm-radius;
    margin: 6px;
    padding: 8px;
  }
  .selRow {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 4px 0;
    &:not(:last-child) {
      border-bottom: 1px solid #d8d8d8;
    }
  }
  .itemWrapper {
    box-shadow: 0 0 15px rgba(#000, .35);
    padding: 16px;
    max-width: $wrapper;
    min-height: 200px;
    margin: 12px auto;
  }
  .itemSelf {
    @include boxSize($md-box);
    margin: 6px;
    font-size: 20px;
    &:nth-child(5n-4) { background-color: indianred; }
    &:nth-child(5n-3) { background-color: darkorange; }
    &:nth-child(5n-2) { background-color: gold;  }
    &:nth-child(5n-1) { background-color: seagreen; }
    &:nth-child(5n)   { background-color: steelblue; }
    &.align-self-stretch {
      height: auto;
    }
  }
  .flex-basis-0 {
    flex-basis: 0 !important;
  }
  .flex-basis-px {
    flex-basis: 100px !important;
  }
  .flex-basis-percent {
    flex-basis: 50% !important;
  }
}

@media (max-width: 768px) {
  body {
    h3 {
      font-size: 1.5rem;
    }
    .boxItem {
      &:nth-child(n+6) {
        display: none;
      }
    }
    .itemSelf {
      @include boxSize($sm-box);
    }
    .selector {
      font-size: 13px;
      margin: 0;
      padding: 4px;
      .numberBox .number {
        width: 30px;
      }
    }
    .itemSelf, .selector {
      &:nth-child(n+4) {
        display: none;
      }
    }
  }
}
</style>
