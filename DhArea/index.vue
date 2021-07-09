<template>
  <el-cascader
    :value="areavalue"
    :options="area_option"
    :props="props"
    separator=" - "
    :size="size"
    style="width: 100%"
    placeholder="省市区"
    @change="handleChange"
  />
  <!-- <el-popover v-model="isShow" trigger="click" popper-class="my-popper" placement="bottom-start" transition="dialog-fade">
    <div class="select-option">
      <div class="option">
        <el-cascader-panel
          :value="areavalue"
          :options="area_option"
          :props="props"
          separator=" - "
          @change="handleChange"
        />
      </div>
    </div>
    <div slot="reference" class="select-label" :style="`height:${getSize}px;line-height:${getSize}px;`">
      <div class="left">
        <span class="label">{{ getAreaText }}</span>
      </div>
      <div class="icon"><i class="el-icon-arrow-down" /></div>
    </div>
  </el-popover> -->
</template>

<script>
import area from './area'
export default {
  name: 'DhArea',
  props: {
    // 值
    province: {
      type: String,
      default: ''
    },
    provinceCode: {
      type: String,
      default: ''
    },
    city: {
      type: String,
      default: ''
    },
    cityCode: {
      type: String,
      default: ''
    },
    area: {
      type: String,
      default: ''
    },
    areaCode: {
      type: String,
      default: ''
    },
    // 展开触发方式
    expandTrigger: {
      type: String,
      default: 'hover'
    },
    checkStrictly: {
      type: Boolean,
      default: false
    },
    // 大小
    size: {
      type: String,
      default: 'medium'
    }
  },
  data() {
    return {
      area_option: area,
      isShow: false
    }
  },
  computed: {
    props() {
      return {
        value: 'value',
        checkStrictly: this.checkStrictly,
        expandTrigger: this.expandTrigger // 展开触发方式
      }
    },
    getAreaText() {
      let area = ''
      if (this.province) {
        area += this.province
      }
      if (this.city) {
        area += '-' + this.city
      }
      if (this.area) {
        area += '-' + this.area
      }
      return area || '省市区'
    },
    areavalue() {
      return [this.province + '-' + this.provinceCode, this.city + '-' + this.cityCode, this.area + '-' + this.areaCode]
    },
    getSize() {
      switch (this.size) {
        case 'small': return 32
        case 'mini': return 28
        case 'medium': return 36
      }
      return 40
    }
  },
  methods: {
    handleChange(e) {
      const result = e.map(v => {
        return { label: v.split('-')[0], value: v.split('-')[1] }
      })
      this.$emit('change', result)
      this.isShow = false
    },
    // 清除选中
    handleClear() {
      this.$emit('change', [])
    }
  }
}
</script>
<style lang="scss">
.my-popper {
  padding: 0!important;
}

</style>
<style lang="scss" scoped>
// 外面文本框
.select-label {
  display: flex;
  align-items: center;
  border-radius: 4px;
  padding: 0 5px;
  font-size: 14px;
  cursor: pointer;
  color: #606266;
  justify-content: space-between;
  border: 1px solid #DCDFE6;
  background-color: #FFFFFF;

  &:focus {
    outline: none;
    border-color: #3784DC;
  }

  // &:hover {
  //   background-color: #f5f5f5;
  // }

  .left {
    display: flex;
  }
  .label {
    width: 100%;
    min-width: 20px;
    color: #333333;
    margin: 0 10px;
    overflow: hidden;
    text-overflow:ellipsis;
    white-space: nowrap;
  }
  .icon {
    display: flex;
    width: 14px;
    height: 100%;
    align-items: center;
    color: #C0C4CC;
  }
}
.select-label-bg {
  background-color: #f5f5f5;
}
// 选择区
.select-option {
  font-size: 14px;

  // 信息区
  .option-top {
    display: flex;
    color: #999999;
    padding: 6px 12px;
    height: 30px;
    font-size: 12px;
    align-items: center;

    .top-line {
      height: 14px;
      border-left: 1px solid #cccccc;
      margin: 0 6px;
    }
    .top-clear {
      color: #00CC88;
      cursor: pointer;
    }
  }
}

@keyframes dialog-fade {
  0% {
    transform: translate3d(0, 100%, 0);
    opacity: 0;
  }
  100% {
    transform: translate3d(0, 0, 0);
    opacity: 1;
  }
}
</style>

