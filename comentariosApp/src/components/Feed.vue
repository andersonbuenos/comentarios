<template>
  <div>
    <div v-for="post in posts" :key="post.id" class="card mt-3">
      <div class="card-body">
        <b-img :src="post.image" alt="Post Image" fluid class="mb-3" />
        <h5 class="card-title">{{ post.user.name }}</h5>
        <p class="card-text">{{ post.caption }}</p>
        <div class="d-flex justify-content-between">
          <button @click="toggleLike(post.id)" :class="{ 'text-danger': post.liked }">
            <i class="bi-heart"></i> {{ post.likes }}
          </button>
          <button @click="toggleComments(post.id)">
            <i class="bi-chat"></i> {{ post.comments.length }}
          </button>
        </div>
        <div v-if="showComments[post.id]">
          <hr />
          <div v-for="comment in post.comments" :key="comment.id">
            <strong>{{ comment.user.name }}:</strong> {{ comment.text }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['posts'],
  data() {
    return {
      showComments: {},
    };
  },
  methods: {
    toggleComments(postId) {
      this.$set(this.showComments, postId, !this.showComments[postId]);
    },
    toggleLike(postId) {
      const post = this.posts.find((p) => p.id === postId);
      post.liked = !post.liked;
      post.likes += post.liked ? 1 : -1;
    },
  },
};
</script>

<style scoped>
.card {
  width: 100%;
  max-width: 600px;
  margin: 0 auto;
}

.card-title {
  font-size: 1.2rem;
  font-weight: bold;
}

.card-text {
  margin-bottom: 1rem;
}

button {
  border: none;
  background: none;
  cursor: pointer;
}

button i {
  font-size: 1.5rem;
  margin-right: 0.5rem;
}

button:hover {
  text-decoration: underline;
}

.bi-heart,
.bi-chat {
  font-size: 1.5rem;
}
</style>
