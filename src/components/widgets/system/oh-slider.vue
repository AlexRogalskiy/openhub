<template>
  <f7-range v-bind="config" :value="value" @range:changed="onChange" />
</template>

<script>
import mixin from '../widget-mixin'

export default {
  name: 'oh-slider',
  mixins: [mixin],
  mounted () {
    delete this.config.value
  },
  computed: {
    value () {
      const value = parseFloat(this.context.store[this.config.item].state)
      return value
    }
  },
  methods: {
    onChange (value) {
      if (value === this.value) return
      this.$store.dispatch('sendCommand', { itemName: this.config.item, cmd: value.toString() })
    }
  }
}
</script>
