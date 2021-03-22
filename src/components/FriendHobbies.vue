<template>
  <HobbiesList
    v-bind="$props"
    v-on="$listeners"
  >
    <template v-slot:item="{ item }">
      <HobbiesListItem
        :item="item"
      >
        <template #prepend>
          <img
            class="add-icon"
            src="../assets/add.gif"
            alt="add"
            @click="addClick(item)"
          >
        </template>
        <template #item>
          {{ item.text }}
        </template>
        <template #tag>
          <span
            v-if="isAlreadyAdded(item)"
            class="tag"
          >
            <img
              src="../assets/ok.png"
              alt="ok"
            >
            Добавенно в ваши увлечения
          </span>
        </template>
        <template #append>
          <div
            class="warn"
            @click="showPrompt"
          >
            <img
              src="../assets/warn.png"
              alt="warning"
            >
            <span>пожаловаться</span>
          </div>
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
    },
    myHobbies: {
      type: Array,
      default: () => []
    },
    withInput: {
      type: Boolean,
      default: false
    }
  },

  methods: {
    isAlreadyAdded (item) {
      return !!this.myHobbies.find(i => i.text === item.text)
    },

    addClick (item) {
      this.$emit('add-click', item)
    },

    showPrompt () {
      prompt('Опишите проблему')
    }
  }
}
</script>

<style lang="scss" scoped>
.add-icon {
  cursor: pointer;
  margin-right: 5px;
}

.warn {
  display: flex;
  align-items: center;
  margin-left: 5px;
  cursor: pointer;

  img {
    margin-right: 5px;
  }
}

.tag {
  margin-left: 5px;
  display: inline-flex;
  align-items: center;

  img {
    margin-right: 5px;
  }
}
</style>
