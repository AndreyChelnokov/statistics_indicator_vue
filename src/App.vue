<template>
  <div id="app">
    <div class="fake-body">
      <div class="statistics">
        <div data-wrap :class="hiddenClass" class="statistics__wrapper">

          <Indicator
              v-for="indicator in data"
              :indicator="indicator"
              @handlerHoverIndicator="hiddenOtherIndicator"
              @handlerExitIndicator="openOtherIndicator"
          />

        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Indicator from './components/indicator'

export default {
  name: 'App',
  data: function () {
    return {
      hiddenClass: '',
      data: [
        {
          name: 'risk_of_loss',
          title: 'Risk of Loss',
          params: [
            {
              name: 'low',
              value: 4
            },
            {
              name: 'average',
              value: 40
            },
            {
              name: 'high',
              value: 300
            },
            {
              name: 'not-rated',
              value: 56
            }
          ]
        },
        {
          name: 'impact_of_loss',
          title: 'Impact of Loss',
          params: [
            {
              name: 'low',
              value: 4
            },
            {
              name: 'average',
              value: 40
            },
            {
              name: 'high',
              value: 250
            },
            {
              name: 'not-rated',
              value: 456
            }
          ]
        },
        {
          name: 'satisfaction',
          title: 'Satisfaction',
          params: [
            {
              name: 'low',
              value: 50
            },
            {
              name: 'average',
              value: 300
            },
            {
              name: 'high',
              value: 50
            }
          ]
        },
        {
          name: 'performance',
          title: 'Performance',
          params: [
            {
              name: 'low',
              value: 394
            },
            {
              name: 'average',
              value: 3
            },
            {
              name: 'high',
              value: 2
            },
            {
              name: 'not-rated',
              value: 1
            }
          ]
        }
      ]
    }
  },
  methods: {
    hiddenOtherIndicator(prop) {
      this.hiddenClass = `transparent-to-all-but-${prop.id}`
    },
    openOtherIndicator() {
      this.hiddenClass = '';
    }
  },
  components: {
    Indicator
  }
}
</script>

<style>
body {
  margin: 0;
  padding: 0;
  box-sizing: border-box;

  font-family: 'Lab Grotesque', sans-serif;
}

.fake-body {
  height: 100vh;
  display: flex;
  align-items: center;
}

.statistics {
  padding: 22px 23px 22px 23px;
  flex-grow: 1;
  max-width: 830px;
  margin: 0 auto;
}
.statistics__wrapper {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  justify-content: space-between;
}
.statistics__wrapper > div {
  width: calc(50% - 16px);
}
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
.indicator__item {
  position: relative;

  flex-grow: 1;

  width: 100%;

  min-width: 8px;

  transition: .5s;
}
.indicator__item-content {
  position: absolute;
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

.indicator__item-top {
  pointer-events: none;
  position: absolute;
  top: 6px;
  font-weight: bold;
  font-size: 14px;
  line-height: 22px;
  width: max-content;
  text-transform: lowercase;
  opacity: 0;

  transition: .5s;
}
.indicator__item-top:first-letter {
  text-transform: uppercase;
}
.indicator__item-bottom {
  pointer-events: none;
  font-size: 14px;
  line-height: 22px;
  color: #1A1A1A;
  width: max-content;
  position: absolute;
  bottom: 6px;
  opacity: 0;

  transition: .5s;
}

.indicator__item:hover {
  cursor: pointer;
}
.indicator__item:hover .indicator__item-top {
  bottom: auto;
  top: -25px;
  opacity: 1;

  transition: .5s;
}
.indicator__item:hover .indicator__item-bottom {
  top: auto;
  bottom: -27px;
  opacity: 1;

  transition: .5s;
}

.transparent-to-all-but-low .indicator__item:nth-child(2),
.transparent-to-all-but-low .indicator__item:nth-child(3),
.transparent-to-all-but-low .indicator__item:nth-child(4){
  opacity: .08;
  transition: .5s;
}
.transparent-to-all-but-average .indicator__item:nth-child(1),
.transparent-to-all-but-average .indicator__item:nth-child(3),
.transparent-to-all-but-average .indicator__item:nth-child(4){
  opacity: .08;
  transition: .5s;
}
.transparent-to-all-but-high .indicator__item:nth-child(1),
.transparent-to-all-but-high .indicator__item:nth-child(2),
.transparent-to-all-but-high .indicator__item:nth-child(4){
  opacity: .08;
  transition: .5s;
}
.transparent-to-all-but-not-rated .indicator__item:nth-child(1),
.transparent-to-all-but-not-rated .indicator__item:nth-child(2),
.transparent-to-all-but-not-rated .indicator__item:nth-child(3){
  opacity: .08;
  transition: .5s;
}

.transparent-to-all-but-risk_of_loss .statistics-item {
  opacity: .08;
  transition: .5s;
}
.transparent-to-all-but-impact_of_loss .statistics-item {
  opacity: .08;
  transition: .5s;
}
.transparent-to-all-but-satisfaction .statistics-item {
  opacity: .08;
  transition: .5s;
}
.transparent-to-all-but-performance .statistics-item {
  opacity: .08;
  transition: .5s;
}

.transparent-to-all-but-performance #performance {
  opacity: 1;
}
.transparent-to-all-but-satisfaction #satisfaction {
  opacity: 1;
}
.transparent-to-all-but-impact_of_loss #impact_of_loss {
  opacity: 1;
}
.transparent-to-all-but-risk_of_loss #risk_of_loss {
  opacity: 1;
}





@media(max-width: 850px) {
  .statistics__wrapper {
    flex-direction: column;
  }
  .statistics__wrapper > div {
    width: 100%;
  }
  .statistics {
    max-width: 400px;
  }
}
</style>
