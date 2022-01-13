<template>
  <div>
    <div :id="indicator.name" class="statistics__item statistics-item">
      <div class="statistics-item__title">{{ indicator.title }}</div>
      <div ref="indicator" :class="hiddenClass" class="statistics-item__indicator indicator">
        <Param
            v-for="param in indicator.params"
            :param="param"
            :onePercent="onePercent"
            @hiddenOtherParam="handlerHoverParam"
            @openOtherParam="handlerExitParam"
        />
      </div>
    </div>
  </div>
</template>

<script>
import Param from '../components/param'
export default {
  name: 'Indicator',
  data() {
    return {
      hiddenClass: '',
    }
  },
  props: {
    indicator: Object
  },
  components: {
    Param
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

<style scoped>
</style>
