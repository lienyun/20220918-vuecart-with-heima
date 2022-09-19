<template>
  <div class="goods-container">
    <div class="left">
      <div class="form-check">
        <input class="form-check-input" type="checkbox" value="" :id="id" :checked="checked" @change="onCheckBoxChange">
        <label class="form-check-label" :for="id">
          <img :src="thumb" alt="商品圖片" class="thumb">
        </label>
      </div>
      
    </div>
    <div class="right">
      <div class="top">{{ title }}</div>
      <div class="bottom">
        <div class="price">{{ price.toFixed(2) }}</div>
        <div class="count">
          <EsCounter :num="count" :min="1" @numChange="getNumber"/>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import EsCounter from '../es-counter/EsCounter.vue'

export default {
  name: 'EsGoods',
  props: {
    //商品的id
    id: {
      type: [String, Number],
      required: true
    },
    //商品的縮圖
    thumb: {
      type: String,
      required: true
    },
    //商品名稱
    title: {
      type: String,
      required: true
    },
    //商品單價
    price: {
      type: Number,
      required: true
    },
    //數量
    count: {
      type: Number,
      required: true
    },
    //勾選狀態
    checked: {
      type: Boolean,
      required: true
    },
  },
  emits: ['stateChange', 'countChange'],
  methods: {
    onCheckBoxChange(e) {
      // console.log(e.target.checked)
      this.$emit('stateChange',{
        id: this.id,
        value: e.target.checked,
      })
    },
    //監聽數量變化
    getNumber(num){
      console.log(num)
      this.$emit('countChange', {
        id: this.id,
        value: num
      })
    }
  },
  components: {
    EsCounter
  }
}
</script>

<style lang="less" scoped>
.goods-container {
  //+是CSS選擇器，選擇緊接連著另一個元素後的元素，兩者有相同的父元素
  +.goods-container {
    border-top: 1px solid #efefef;
  }
  display: flex;
  padding: 10px;
}

.left {
  margin-right: 10px;
}

.thumb {
  display: block;
  width: 100px;
  height: 100px;
  background-color: #efefef;
}

.right {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  flex: 1;
}

.top {
  font-weight: bold;
}

.bottom {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.price {
  color: red;
  font-weight: bold;
}

.form-check-input{
  margin-top: 3.4rem;
}
</style>