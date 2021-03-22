<template>
  <div
    class="root"
    @mouseenter="toggleControlsVisibility"
    @mouseleave="toggleControlsVisibility"
  >
    <div class="prepend">
      <slot
        v-if="isControlsVisible"
        name="prepend"
        :item="item"
      />
    </div>

    <div
      ref="text"
      class="text"
    >
      <template v-if="$scopedSlots.item">
        <slot
          name="item"
          :item="item"
        />

        <template v-if="$slots.tag">
          <br v-if="isOverflowed">
          <slot name="tag" />
        </template>
      </template>
      <template v-else>
        {{ item.text }}
      </template>
      <div
        v-if="isOverflowed"
        class="fade"
      />
    </div>

    <div class="append">
      <slot
        v-if="isControlsVisible"
        name="append"
        :item="item"
      />
    </div>
  </div>
</template>

<script>
export default {
  props: {
    item: {
      type: Object,
      required: true
    }
  },

  data () {
    return {
      isControlsVisible: false,
      isMounted: false
    }
  },

  computed: {
    isOverflowed () {
      if (this.isMounted) {
        const el = this.$refs.text
        return (el.offsetHeight < el.scrollHeight || el.offsetWidth < el.scrollWidth)
      }

      return false
    }
  },

  mounted () {
    this.isMounted = true
  },

  methods: {
    toggleControlsVisibility () {
      this.isControlsVisible = !this.isControlsVisible
    }
  }
}
</script>

<style lang="scss" scoped>
.root {
  display: flex;
  align-items: center;
  padding: 5px;
  margin-bottom: 5px;

  .prepend {
    display: flex;
    align-items: center;
  }

  .text {
    display: flex;
    align-items: center;
    flex-wrap: wrap;
    position: relative;
    flex-grow: 1;
    overflow: hidden;
    white-space: nowrap;

    .fade {
      position: absolute;
      width: 15px;
      height: 100%;
      right: 0;
      top: 0;
      background-image: url("../assets/fader.png");
      background-repeat: repeat-y;
    }
  }

  .append {

  }
}
</style>
