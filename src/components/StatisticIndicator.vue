<template>
  <div>
    <div :id="indicator.name" class="statistics__item statistics-item">
      <div class="statistics-item__title">{{ indicator.title }}</div>
      <div ref="indicator" :class="hiddenClass" class="statistics-item__indicator indicator">
        <IndicatorParam
            v-for="param in indicator.params"
            :key="param.name"
            :param="param"
            :one-percent="onePercent"
            @hiddenOtherParam="handlerHoverParam"
            @openOtherParam="handlerExitParam"
        />
      </div>
    </div>
  </div>
</template>

<script>
import IndicatorParam from './IndicatorParam'
export default {
  name: 'StatisticIndicator',
  data() {
    return {
      hiddenClass: '',
    }
  },
  props: {
    indicator: {
      type: Object,
      required: true,
      // validator: function (value) {
      //   const possibleNamesParams = [ 'low', 'average', 'high', 'not-rated' ];
      //   const isMatchNames = value.params.map(param => {
      //     return possibleNamesParams.indexOf(param.name) !== -1 ? true : false
      //   }).filter(Boolean).length > 0;
      //
      //   return value.params.length && value.name && isMatchNames;
      // }
    }
  },
  components: {
    IndicatorParam
  },
  methods: {
    handlerHoverParam(prop) {
      this.hiddenOtherParam(prop)
      this.$emit('handlerHoverIndicator', { id: this.indicator.name })
    },
    handlerExitParam() {
      this.openOtherParam()
      this.$emit('handlerExitIndicator')
    },
    hiddenOtherParam(prop) {
      this.hiddenClass = prop
    },
    openOtherParam() {
      this.hiddenClass = ''
    }
  },
  computed: {
    totalCount() {
      return this.indicator.params.map(item => item.value).reduce(function(sum, arg) {
        return sum + (parseInt(arg) || 0);
      }, 0)
    },
    onePercent() {
      return this.totalCount / 100;
    }
  }
}
</script>

<style>

  .statistics-item {
    display: flex;
    align-items: center;
    padding: 10px 0;
    box-sizing: border-box;
    justify-content: space-between;
    transition: .5s;
  }
  .indicator__item:not(:last-child) {
    border-right: 1px solid #fff;
  }
  .statistics-item__title {
    font-size: 16px;
    line-height: 24px;
    color: #1A1A1A;
  }
  .statistics-item__indicator{
    margin-left: 19px;
  }

  .indicator {
    display: flex;

    width: 100%;
    height: 6px;

    max-width: 274px;

    border-radius: 4px;

    position: relative;

    /*overflow: hidden;*/
  }
</style>
