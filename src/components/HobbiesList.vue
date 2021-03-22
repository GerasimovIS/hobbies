<template>
  <div>
    <template v-if="$slots.title">
      <slot name="title" />
    </template>
    <template v-else>
      <h2>{{ title }}</h2>
    </template>
    <hr class="hr">
    <div class="hobbies">
      <div class="title">
        <h3 class="content">
          Хобби
        </h3>
      </div>
      <div class="hobbies-list">
        <div
          v-if="withInput"
          class="hobbies-list-input"
        >
          <input
            v-model="inputText"
            type="text"
            placeholder="Введите текст"
            @keypress.enter="addHobby"
          >
        </div>
        <div class="hobbies-items">
          <div
            v-for="item in displayListData"
            :key="item.id"
            class="hobbies-items__item"
          >
            <slot
              name="item"
              :item="item"
            >
              {{ item.text }}
            </slot>
          </div>
          <template v-if="tailLength > 0">
            <div v-if="!isTailShowed">
              <a
                href="#"
                @click.prevent="toggleTailVisibility"
              >
                еще {{ tailLength }} {{ declOfNum(tailLength, ['интерес', 'интереса', 'интересов']) }}
              </a>
            </div>
            <div v-else>
              <a
                href="#"
                @click.prevent="toggleTailVisibility"
              >
                показать меньше
              </a>
            </div>
          </template>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
function declOfNum (number, titles) {
  const cases = [2, 0, 1, 1, 1, 2]
  return titles[(number % 100 > 4 && number % 100 < 20) ? 2 : cases[(number % 10 < 5) ? number % 10 : 5]]
}

export default {
  props: {
    title: {
      type: String,
      default: ''
    },

    value: {
      type: Array,
      default: () => []
    },

    withInput: {
      type: Boolean,
      default: true
    }
  },

  data () {
    return {
      inputText: '',
      isTailShowed: false
    }
  },

  computed: {
    displayListData () {
      return this.isTailShowed
        ? this.value
        : this.value.slice(0, 2)
    },

    tailLength () {
      return this.value.length - 2
    }
  },

  methods: {
    declOfNum,

    addHobby () {
      if (this.inputText) {
        const newHobby = { id: Date.now(), text: this.inputText }

        this.$emit('input', [newHobby, ...this.value])
        this.inputText = ''
      }
    },

    toggleTailVisibility () {
      this.isTailShowed = !this.isTailShowed
    }
  }
}
</script>

<style lang="scss" scoped>
.hr {
  border: none;
  border-top: 2px solid #333;
  color: #333;
  overflow: visible;
  text-align: center;
  margin: 0;

  &--dotted {
    border-top: 2px dotted #333;
  }
}

.hobbies {
  .title {
    display: flex;
    align-items: center;

    .content {
      padding-right: 15px;
    }

    .hr {
      flex-grow: 1;
    }
  }
}

.hobbies-list {
  padding: 15px;
}

.hobbies-list-input {
  input {
    padding: 5px;
  }

  margin-bottom: 15px;
}
</style>
