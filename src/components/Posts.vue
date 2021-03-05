<template>
  <h2>投稿する</h2>
  <ul>
    <li v-for="post in posts" :key='post.id'>
      <p>{{ post.name }}</p>
      <p>{{ post.comment }}</p>
      <input type="button" value="編集" @click="update(post)"/>
      <input type="button" value="削除" @click="remove(post)" />
    </li>
  </ul>
</template>

<script>
export default {
  data() {
    return {
      posts: []
    }
  },

  created() {
    this.read()
  },

  methods: {
    // 一覧画面
    read() {
      fetch('http://localhost:3000/posts')
        .then( res => res.json() )
        .then( res => this.posts = res )
    },

    // 追加
    add() {

    },

    // 編集
    update() {

    },

    // 削除
    remove() {

    }
  }
}
</script>

<style>

</style>