<template>
  <div>
    <div class="indicator__item-top"><span>{{ name }}</span> - {{ currentPercent }}%</div>
    <div class="indicator__item-bottom">{{ value }} employees</div>
  </div>
</template>

<script>
export default {
  name: 'ParamLabel',
  props: {
    name: {
      type: String,
      required: true,
      validator: function (value) {
        return [ 'low', 'average', 'high', 'not-rated' ].indexOf(value) !== -1
      }
    },
    currentPercent: {
      type: Number,
      required: true,
      validator: function (value) {
        return 0 <= value <= 100
      }
    },
    value: {
      type: Number,
      required: true,
    }
  },
  methods: {

  },
  mounted() {
  }
}
</script>

<style>
  .indicator__item-top {
    pointer-events: none;
    top: 6px;
    font-weight: bold;
    font-size: 14px;
    line-height: 22px;
    width: max-content;
    text-transform: lowercase;
    opacity: 0;
    display: inline-block;

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
    bottom: 6px;
    opacity: 0;
    display: inline-block;

    transition: .5s;
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
</style>
