<template>
  <div id="app" class="container mt-4">
    <div class="row">
      <div class="col-md-12">
        <div class="card" v-for="(post, index) in posts" :key="index">
          <div class="row">
            <div class="col-md-6">
              <div class="card-header">
                <img :src="post.profilePicture" class="profile-pic" alt="Profile" />
                <span class="username">{{ post.username }}</span>
              </div>
              <img :src="post.image" class="card-img-top" alt="Post" />
              <div class="card-body">
                <button @click="toggleLike(index)" class="btn btn-like" :class="{ 'liked': post.liked }">
                  <i class="bi-heart"></i> {{ post.likes }}
                </button>
              </div>
            </div>
            <div class="col-md-6">
              <div class="comments">
                <div v-for="(comment, cIndex) in post.comments.slice(0, 5)" :key="cIndex" class="comment">
                  <img :src="comment.profilePicture" class="comment-profile-pic" alt="Profile" />
                  <span class="username">{{ comment.username }}</span>
                  <span>{{ comment.text }}</span>
                </div>
              </div>
              <div class="comment-input">
                <input v-model="newComment" @keyup.enter="addComment(index)" class="form-control instagram-comment-input" placeholder="Adicione um comentário..." />
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import 'bootstrap-icons/font/bootstrap-icons.css';

export default {
  data() {
    return {
      posts: [
        {
          username: 'Htinha',
          profilePicture: 'https://placekitten.com/40/41',
          image: 'https://placekitten.com/600/400',
          liked: false,
          likes: 0,
          comments: [],
        },
      ],
      newComment: '',
    };
  },
  methods: {
    toggleLike(index) {
      this.posts[index].liked = !this.posts[index].liked;
      this.posts[index].likes += this.posts[index].liked ? 1 : -1;
    },
    addComment(index) {
      const commentText = this.newComment.trim();
      if (commentText !== '') {
        const commentUser = `user${this.posts[index].comments.length + 1}`;
        const commentProfilePicture = `https://placekitten.com/40/40?random=${this.posts[index].comments.length + 1}`;
        
        this.posts[index].comments.push({
          username: commentUser,
          profilePicture: commentProfilePicture,
          text: commentText,
        });
        this.newComment = '';
      }
    },
  },
};
</script>

<style>
.profile-pic {
  border-radius: 50%;
  margin-right: 10px;
}

.comment-profile-pic {
  border-radius: 50%;
  margin-right: 5px;
}

.username {
  font-weight: bold;
}

.card {
  margin-bottom: 20px;
}

.btn-like {
  border: none;
  background: none;
  cursor: pointer;
}

.btn-like i {
  font-size: 1.5rem;
  margin-right: 0.5rem;
}

.btn-like:hover {
  text-decoration: underline;
}

.btn-like.liked {
  color: red;
}

.comments {
  margin-top: 10px;
}

.comment {
  margin-bottom: 5px;
  display: flex;
  align-items: center;
}

/*.comment-input {
  margin-top: 10px;
  border: none; 
  padding: 8px;
  width: 100%;
  font-size: 1rem;
}*/

.instagram-comment-input {
  border: none !important;
  margin-top: 10px;
  border-top: 1px solid #ccc; 
  padding: 8px;
  width: 100%;
  font-size: 1rem;
  resize: none; 
  border-bottom-style: none;
}

.instagram-comment-input.hover {
  border: none!important;
}
</style>
