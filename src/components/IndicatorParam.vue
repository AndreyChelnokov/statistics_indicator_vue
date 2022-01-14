<template>
  <div
      @mouseenter="hiddenOtherParam"
      @mouseleave="openOtherParam"
      :data-params="param.name" :style="{ maxWidth: widthParam + '%' }"
      :class="'indicator__item indicator__item_' + param.name"
  >
    <div ref="label" :data-float="float" class="indicator__item-content">
      <ParamLabel
          :name="param.name"
          :current-percent="currentPercent"
          :value="param.value"
      />
    </div>

  </div>
</template>

<script>
import ParamLabel from "./ParamLabel";
export default {
  name: 'IndicatorParam',
  data() {
    return {
      float: ''
    }
  },
  props: {
    param: {
      type: Object,
      required: true,
      validator: function (value) {
        const isMatchNames = [ 'low', 'average', 'high', 'not-rated' ].indexOf(value.name) !== -1
        const isMatchValue = Number.isInteger(value.value)

        return isMatchNames && isMatchValue;
      }
    },
    onePercent: {
      type: Number,
      required: true,
      validator: function (value) {
        return value > 0;
      }
    }
  },
  components: {
    ParamLabel
  },
  methods: {
    hiddenOtherParam() {
      this.$emit('hiddenOtherParam', `transparent-to-all-but-${this.param.name}`)
    },
    openOtherParam() {
      this.$emit('openOtherParam')
    },
    getWidthParamContent() {
      return this.$refs.label.clientWidth;
    },
    getWidthParam() {
      return this.$el ? this.$el.clientWidth : 0;
    },
    getOffsetLeftParam() {
      return this.$el ? this.$el.offsetLeft : 0;
    },
    getFloatContent() {
      const widthContent = this.getWidthParamContent();
      const widthParam = this.getWidthParam();
      const offsetParam = this.getOffsetLeftParam();

      if (widthParam <= widthContent) {
        if (offsetParam >= this.$el.parentNode.clientWidth / 2) {
          return 'right'
        }
        return 'left'
      }
      return 'left'
    }
  },
  computed: {
    currentPercent() {
      return Math.floor(this.widthParam)
    },
    widthParam() {
      return this.param.value / this.onePercent
    }
  },
  mounted() {
    this.float = this.getFloatContent();
  }
}
</script>


<style>
  [data-float="right"] {
    right: 0;
    transform: translateY(-50%);
    text-align: right;
  }
  [data-float="left"] {
    left: 0;
    transform: translateY(-50%);
    text-align: left;
  }
  [data-float="left"] > div {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
  }
  [data-float="right"] > div {
    display: flex;
    flex-direction: column;
    align-items: flex-end;
  }
  .indicator__item-content {
    height: 60px;
    top: 4px;
  }
  .indicator__item-content > div {
    height: 100%;
    justify-content: space-between;
  }


  .indicator__item {
    position: relative;

    flex-grow: 1;

    width: 100%;

    min-width: 8px;

    transition: .5s;
  }
  .indicator__item-content {
    position: absolute;
    pointer-events: none;
  }

  .indicator__item:first-child {
    border-top-left-radius: 4px;
    border-bottom-left-radius: 4px;
  }
  .indicator__item:last-child {
    border-top-right-radius: 4px;
    border-bottom-right-radius: 4px;
  }
  .indicator__item_low {
    background-color: #45E596;
    color: #45E596;
  }
  .indicator__item_average {
    background-color: #FFC44C;
    color: #FFC44C;
  }
  .indicator__item_high {
    background-color: #FF4C4C;
    color: #FF4C4C;
  }
  .indicator__item_not-rated {
    background-color: #F2F2F2;
    color: #F2F2F2;
  }
  .indicator__item_not-rated:hover {
    background-color: #808080;
    color: #808080;
  }

  .indicator__item:hover {
    cursor: pointer;
  }
</style>
