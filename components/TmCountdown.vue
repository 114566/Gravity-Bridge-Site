<template>
  <div v-if="isCountingDown">
    <span class="tm-code">
      {{ days }}:{{ hours }}:{{ minutes }}:{{ seconds }}
    </span>
  </div>
</template>

<script>
export default {
  props: {
    now: {
      type: Number,
      default: null,
    },
    end: {
      type: String,
      default: '',
    },
  },
  computed: {
    isCountingDown() {
      return (
        this.days > 0 || this.hours > 0 || this.minutes > 0 || this.seconds > 0
      )
    },
    endDate() {
      return Math.trunc(Date.parse(this.end) / 1000)
    },
    seconds() {
      const value = (this.endDate - this.now) % 60
      if (value < 10) return '0' + value
      return value
    },
    minutes() {
      const value = Math.trunc((this.endDate - this.now) / 60) % 60
      if (value < 10) return '0' + value
      return value
    },
    hours() {
      const value = Math.trunc((this.endDate - this.now) / 60 / 60) % 24
      if (value < 10) return '0' + value
      return value
    },
    days() {
      const value = Math.trunc((this.endDate - this.now) / 60 / 60 / 24)
      if (value < 10) return '0' + value
      return value
    },
  },
}
</script>

<style lang="stylus"></style>
