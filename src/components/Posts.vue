<template>
  <h2>投稿する</h2>
  <h2>{{ posts }}</h2>
  <ul>
    <li v-for="post in posts" :key='post.id'>
      <input type="text" v-model="post.name" />
      <textarea v-model="post.comment"></textarea>
      <p>{{ post.name }}</p>
      <p>{{ post.comment }}</p>
      <input type="button" value="編集" @click="update(post)"/>
      <input type="button" value="削除" @click="remove(post)" />
    </li>
  </ul>
  <input type="text" v-model="new_post.name">
  <textarea v-model="new_post.comment"></textarea>
  <input type="button" value="追加" @click="create">
</template>

<script>
export default {
  data() {
    return {
      posts: [],
      new_post: {
        id: 0,
        name: null,
        comment: null
      }
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
    create() {
      fetch('http://localhost:3000/posts', {
        method: 'POST',
        body: JSON.stringify({
          id: this.new_post.id + 1,
          name: this.new_post.name,
          comment: this.new_post.comment
        }),
        headers: new Headers({ 'Content-type' : 'application/json' })
      })
        .then( () => {
          this.posts.push({
            id: this.new_post.id,
            name: this.new_post.name,
            comment: this.new_post.comment
          })
          this.new_post = []
        })
    },

    // 編集
    update(post) {
      fetch(`http://localhost:3000/posts/${post.id}`, {
        method: 'PUT',
        body: JSON.stringify({
          name: post.name,
          comment: post.comment
        }),
        headers: new Headers({ 'Content-type' : 'application/json' })
      })
    },

    // 削除
    remove(post) {
      fetch(`http://localhost:3000/posts/${post.id}`, {
        method: 'DELETE'
      })
        .then( () => {
          this.posts = this.posts.filter(item => item !== post)
        })
    }
  }
}
</script>

<style>

</style>