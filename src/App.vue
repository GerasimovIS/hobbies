<template>
  <div class="container">
    <MyHobbies
      v-model="myHobbiesList"
      title="Мои хобби"
    />

    <br>

    <FriendHobbies
      title="Хобби друга"
      :value="friendsHobbiesList"
      :my-hobbies="myHobbiesList"
      @add-click="addToMyHobbiesList"
    />
  </div>
</template>

<script>
import MyHobbies from '@/components/MyHobbies'
import FriendHobbies from '@/components/FriendHobbies'

export default {
  name: 'App',

  components: {
    MyHobbies,
    FriendHobbies
  },

  data () {
    return {
      myHobbiesList: [
        { id: 1, text: 'Готовка' },
        { id: 2, text: 'Программирование' },
        { id: 3, text: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus ad, aperiam asperiores consequuntur debitis ducimus eum, ipsum maiores mollitia odio porro quaerat quasi, sint sit veritatis! Cum esse illum nisi quidem totam. At eius non quaerat veniam voluptatibus voluptatum. Architecto enim eveniet illo incidunt itaque nam nisi placeat quae quam.' }
      ],
      friendsHobbiesList: [
        { id: 1, text: 'Test' },
        { id: 2, text: 'Hello world' },
        { id: 3, text: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus ad, aperiam asperiores consequuntur debitis ducimus eum, ipsum maiores mollitia odio porro quaerat quasi, sint sit veritatis! Cum esse illum nisi quidem totam. At eius non quaerat veniam voluptatibus voluptatum. Architecto enim eveniet illo incidunt itaque nam nisi placeat quae quam.' }
      ]
    }
  },

  methods: {
    addToMyHobbiesList (item) {
      const transferItem = { ...item, id: Date.now() }
      this.myHobbiesList = [transferItem, ...this.myHobbiesList]
    }
  }
}
</script>

<style lang="scss">
* {
  box-sizing: border-box;
}

body, html {
  margin: 0;
  padding: 0;
}

.container {
  max-width: 980px;
  width: 100%;
  margin: 0 auto;
  font-family: Helvetica, Arial, sans-serif;
  padding: 0 15px;
}
</style>
