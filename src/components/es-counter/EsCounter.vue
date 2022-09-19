<template>
  <div class="counter-container">
    <button type="button" class="btn btn-light btn-sm" @click="onSubClick">-</button>
    <input type="number" class="form-control form-control-sm ipt-num" v-model.number.lazy="number" />
    <button type="button" class="btn btn-light btn-sm" @click="onAddClick">+</button>
  </div>
</template>

<script>
export default {
  name: 'Escounter',
  props: {
    num: {
      type: Number,
      default: 0
    },
    min: {
      type: Number,
      default: NaN
    }
  },
  data() {
    return {
      number: this.num
    }
  },
  emits: ['numChange'],
  watch: {
    number(newVal) {
      const parseResult = parseInt(newVal)

      if (isNaN(parseResult) || parseResult < 1) {
        this.number = 1
        return
      }
      if(String(newVal).indexOf('.') !== -1){
        this.number = parseResult
        return
      }
      //觸發自訂事件，把最新的number傳送給使用者
      this.$emit('numChange',this.number)

    }
  },
  methods: {
    onSubClick() {
      if (!isNaN(this.min) && this.number - 1 < this.min) return
      this.number--
    },
    onAddClick() {
      this.number++
    }
  }
}
</script>

<style lang="less" scoped>
.counter-container {
  display: flex;

  .btn {
    width: 25px;
  }

  .ipt-num {
    width: 34px;
    text-align: center;
    margin: 0 4px;
  }
}
</style>