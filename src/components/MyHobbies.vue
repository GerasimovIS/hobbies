<template>
  <HobbiesList
    v-bind="$props"
    v-on="$listeners"
  >
    <template #item="{ item }">
      <HobbiesListItem
        :item="item"
      >
        <template #prepend>
          <img
            class="clear-icon"
            src="../assets/close.png"
            alt="clear"
            @click="removeItem(item)"
          >
        </template>
      </HobbiesListItem>
    </template>
  </HobbiesList>
</template>

<script>
import HobbiesList from '@/components/HobbiesList'
import HobbiesListItem from '@/components/HobbiesListItem'

export default {
  components: {
    HobbiesList,
    HobbiesListItem
  },

  props: {
    title: {
      type: String,
      default: ''
    },
    value: {
      type: Array,
      default: () => []
    }
  },

  methods: {
    removeItem (item) {
      this.$emit('input', this.value.filter(i => i.id !== item.id))
    }
  }
}
</script>

<style lang="scss" scoped>
.clear-icon {
  cursor: pointer;
  margin-right: 5px;
}
</style>
