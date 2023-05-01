<script setup>
let message = ref('')
let CommentStore = ref()

let { data: comments } = useAsyncData('comment', () =>
  $fetch('http://localhost:3004/comments')
)
CommentStore.value = comments.value
function addData() {
  if (message.value != '') {
    const commentData = {
      _id: '',
      picture: '',
      auther: '',
      gender: '',
      comment: message.value,
      liked: true,
      isActive: true,
    }
    CommentStore.value.push(commentData)
    message.value = ''
  }
}
</script>
<template>
  <div class="ms-5">
    <div class="d-block">
      <input v-model="message" type="text" name="comment" class="m-3" />
      <button @click="addData()">Comment</button>
    </div>
    <div v-for="(item, index) in comments" :key="index">
      <Comment
        v-bind="{
          comment: item.comment,
          replies: item.comments,
        }"
      />
    </div>
  </div>
</template>
<style scoped></style>
