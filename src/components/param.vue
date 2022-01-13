<template>
  <div
      @mouseenter="hiddenOtherParam"
      @mouseleave="openOtherParam"
      :data-params="param.name" :style="{ maxWidth: widthParam + '%' }"
      :class="'indicator__item indicator__item_' + param.name">
    <div ref="top"
         :style="{ left: leftPosition, right: rightPosition }"
         class="indicator__item-top"><span>{{ param.name }}</span> - {{ Math.floor(widthParam) }}%</div>
    <div ref="bottom"
         :style="{ left: leftPosition, right: rightPosition }"
         class="indicator__item-bottom">{{ param.value }} employees</div>
  </div>
</template>

<script>
export default {
  name: 'Param',
  data() {
    return {
      float: ''
    }
  },
  props: {
    param: Object,
    onePercent: Number
  },
  methods: {
    hiddenOtherParam() {
      this.$emit('hiddenOtherParam', `transparent-to-all-but-${this.param.name}`)
    },
    openOtherParam() {
      this.$emit('openOtherParam')
    },
    getWidthParamContent() {
      return this.$refs.top.clientWidth > this.$refs.bottom.clientWidth ? this.$refs.top.clientWidth : this.$refs.bottom.clientWidth;
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
    widthParam() {
      return this.param.value / this.onePercent
    },
    rightPosition() {
      return this.float == 'right' ? '0' : 'auto'
    },
    leftPosition() {
      return this.float == 'left' ? '0' : 'auto'
    }
  },
  mounted() {
    this.float = this.getFloatContent();
  }
}
</script>
