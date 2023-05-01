<script setup>
let message = ref('')
let isReply = ref(false)

const props = defineProps({
  comment: {
    type: String,
    required: true,
  },
  replies: {
    type: Array,
    default: () => [],
  },
})

//change isreply value
const changeInput = () => {
  isReply.value = !isReply.value
}

function addData() {
  const commentData = {
    _id: '',
    picture: '',
    auther: '',
    gender: '',
    comment: message.value,
    liked: true,
    isActive: true,
  }
  this.props.replies.push(commentData)
  message.value = ''
  isReply.value = !isReply.value
}
</script>

<template>
  <div class="m-3">
    <p>{{ comment }}</p>
    <button @click="changeInput()">Reply</button>
    <div v-show="isReply">
      <input v-model="message" type="text" name="comment" class="m-3" />
      <button @click="addData()">Add Comment</button>
    </div>
    <div v-for="item in replies" :key="item">
      <ul>
        <Comment
          v-bind="{
            comment: item.comment,
            replies: item.comments,
          }"
        />
      </ul>
    </div>
  </div>
</template>
