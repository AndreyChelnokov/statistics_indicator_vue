<template>
  <div id="app">
    <div class="fake-body">
      <div class="statistics">
        <div data-wrap :class="hiddenClass" class="statistics__wrapper">

          <StatisticIndicator
              v-for="indicator in data"
              :key="indicator.id"
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
import StatisticIndicator from './components/StatisticIndicator'

export default {
  name: 'App',
  data: function () {
    return {
      hiddenClass: '',
      data: [
        {
          id: 1,
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
          id: 2,
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
          id: 3,
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
          id: 4,
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
    StatisticIndicator
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
