### 【class與style綁定】
- class___物件型
```html
<div class="static" v-bind:class="{ 'class-a': isA, 'class-b': isB }"></div>
```

- class___純數組型
```html
<div v-bind:class="[classA, classB]">
```

- class___數組型+三元
```html
<div v-bind:class="[classA, isB ? classB : '']">
```

- class___數組型包物件型
```html
<div v-bind:class="[classA, { classB: isB, classC: isC }]">
```

-  ★ ★ ★Vue style要自己補單位，不過會自動幫忙加前綴
- style___物件型
```html
<div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>
<div v-bind:style="styleObject"></div>
```

- style___陣列型
```html
<div v-bind:style="[styleObjectA, styleObjectB]">
```
****
### 【transition】
- 為.className-transition, .className-enter 和 .className-leave 添加 CSS 规则
-  ★ transition="className" ， 不用綁定；用綁定的話表示值是變數
- [vue-animated-list](https://github.com/vuejs/vue-animated-list)
  CDN 方式試不出來
- 預設transition
```html
 <transition>
      <!-- 這裡透過 v-show 來控制顯示或隱藏 -->
      <div class="block" v-show="isShow">HELLO VUE</div>
    </transition>
```
```css

.v-enter-active, .v-leave-active {
  transition: opacity 1s;
}

.v-enter-from, .v-leave-to {
  opacity: 0;
}

.v-enter-to, .v-leave-from {
  opacity: 1;
}
```

- 命名transition
```html
      <transition name="fade">
        <div class="block" v-show="isShow">HELLO VUE<br>Fade</div>
      </transition>
```
```css
    .fade-enter-active,
    .fade-leave-active {
      transition: opacity 1s;
    }

    .fade-enter-from,
    .fade-leave-to {
      opacity: 0;
    }

    .fade-enter-to,
    .fade-leave-from {
      opacity: 1;
    }
```

- transition mode：mode="out-in"、mode="in-out"
- <transition-group>
- transition =>(O) v-if v-else v-else...  ；(X)v-if  v-if v-if...  、(O):is
  transition-group=> (O)v-if  v-if v-if...也可以
- v-move
- 與其他 CSS 工具庫搭配 - Animate.css


****
### 【animation】
- 無需添加 <transition> 元件
- @animationend="recoveryHandly" 事件，可以回復動畫初始狀態，這樣可以重複觸發動畫執行 
```html
<div id="app">
  <button @click="noActivated = true">Shack It!</button>
  <div class="block" :class="{ shake: noActivated }">Block</div>
  <div class="block" :class="{ shake: noActivated }" @animationend="reactivated">Block</div>
</div>
```
```css   
button {
  font-size: 1rem;
}

.block {
  display: block;
  width: 120px;
  height: 80px;
  line-height: 80px;
  text-align: center;
  font-size: 1.2rem;
  margin-top: 1rem;
  background-color: #3eaf7c;
  color: #fff;
}

.shake {
  animation: shake 0.82s cubic-bezier(0.36, 0.07, 0.19, 0.97) both;
  transform: translate3d(0, 0, 0);
  backface-visibility: hidden;
  perspective: 1000px;
}

@keyframes shake {
  10%,
  90% {
    transform: translate3d(-1px, 0, 0);
  }

  20%,
  80% {
    transform: translate3d(2px, 0, 0);
  }

  30%,
  50%,
  70% {
    transform: translate3d(-4px, 0, 0);
  }

  40%,
  60% {
    transform: translate3d(4px, 0, 0);
  }
}
```
```javascript
new Vue({
  el: "#app",
  data() {
    return {
      noActivated: false
    }
  },
  methods: {
    reactivated() {
      this.noActivated = false;
    }
  }

})
```
****
### 【寶藏】
- [重新認識 Vue.js | Kuro Hsu](https://book.vue.tw/preface.html#%E7%82%BA%E4%BB%80%E9%BA%BC%E8%A6%81%E5%AF%AB%E9%80%99%E6%9C%AC%E6%9B%B8)
- [分享8個非常實用的Vue自定義指令](https://github.com/Michael-lzg/v-directives)

****
### 【觀念】
- [如何理解Vue組件中所說的is特性?](https://segmentfault.com/q/1010000007205176)
- [[補充] 當陣列的內容變動，畫面為何沒更新？ (Vue 2.x)](https://book.vue.tw/CH1/1-6-conditions-and-flow-control.html#%E8%A3%9C%E5%85%85-%E7%95%B6%E9%99%A3%E5%88%97%E7%9A%84%E5%85%A7%E5%AE%B9%E8%AE%8A%E5%8B%95-%E7%95%AB%E9%9D%A2%E7%82%BA%E4%BD%95%E6%B2%92%E6%9B%B4%E6%96%B0-vue-2-x)
- [透過 x-template 封裝模板](https://book.vue.tw/CH2/2-1-components.html#%E9%80%8F%E9%81%8E-x-template-%E5%B0%81%E8%A3%9D%E6%A8%A1%E6%9D%BF)
- [子元件的 data 必須是函數](https://book.vue.tw/CH2/2-1-components.html#%E5%AD%90%E5%85%83%E4%BB%B6%E7%9A%84-data-%E5%BF%85%E9%A0%88%E6%98%AF%E5%87%BD%E6%95%B8)，不然會共用同一個狀態，資料會覆蓋、互相污染