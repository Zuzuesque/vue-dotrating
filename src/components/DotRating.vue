<template lang="pug">
  span.dot-rating
    span(v-for="dot in dots")
      span.dot(@click="dotClicked(dot.rating)") {{dot.symbol}}
</template>

<script>
export default {
  name: 'dot-rating',
  props: {
    id: {
      type: String
    },
    maxValue: {
      type: Number,
      default: 5
    },
    minValue: {
      type: Number,
      default: 0
    },
    startValue: {
      type: Number,
      default: 0
    },
    unselectedSymbol: {
      type: String,
      default: '⚪'
    },
    selectedSymbol: {
      type: String,
      default: '⚫'
    }
  },
  data () {
    return {
      value: this.startValue
    }
  },
  computed: {
    dots: function () {
      var dotData = []
      // generate dot selection
      for (var i = 0; i < this.maxValue; i++) {
        var dot = {}
        dot.rating = i + 1
        // set dot design based on value
        if (dot.rating <= this.value) {
          dot.symbol = this.selectedSymbol
        } else {
          dot.symbol = this.unselectedSymbol
        }
        dotData.push(dot)
      }
      return dotData
    }
  },
  methods: {
    dotClicked: function (rating) {
      // set new value
      if (rating >= this.minValue) {
        if (this.value === 1 && rating === 1 && rating !== this.minValue) {
          this.value = 0
        } else {
          this.value = rating
        }
      }
      // alert parent
      this.$emit('update:startValue', this.value)
    }
  }
}
</script>

<style scoped>
.dot-rating {
  -webkit-touch-callout: none;
  -webkit-user-select: none;
  -khtml-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
span {
  cursor: pointer;
}
</style>
