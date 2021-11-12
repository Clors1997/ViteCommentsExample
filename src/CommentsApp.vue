<template>
  <main class="p-4 bg-gray-50 min-h-screen">
      <div class="max-w-screen-xl mx-auto p-8 rounded-lg shadow-2xl bg-white">
        <h2 class="text-3xl my-6">评论</h2>

        <!-- 评论表单 -->
        <CommentBox @submit="addNewCommend" />  

        <!-- 分隔线 -->
        <DividerHorizontal />
        <div v-for="comment in comments" :key="comment.id">
          <!-- 单个留言 -->
          <CommentItem :user="comment.user" :avatar="comment.avatar" :time="comment.time" :content="comment.content" />
          <!-- 回复列表 -->
          <ReplyContainer v-if="comment.replies">
            <CommentItem v-for="reply in comment.replies" :key="reply.id" :user="reply.user" :avatar="reply.avatar" :time="reply.time" :content="reply.content" />
          </ReplyContainer>
          <!-- 回复 -->
          <ReplayBox @submit="addReply($event, comment.id)" />
        </div>
      </div>
    </main>
</template>

<script setup>
import { ref } from '@vue/reactivity';

import CommentBox from './components/CommentBox.vue';
import DividerHorizontal from './components/DividerHorizontal.vue';
import CommentItem from './components/CommentItem.vue';
import ReplyContainer from './components/ReplyContainer.vue';
import ReplayBox from './components/ReplayBox.vue';

import face from './assets/favicon.svg';

const rid = ref(4);

const comments = ref([
  {
    id: 1,
    user: "梦落轻巡",
    avatar: face,
    time: "2 小时前",
    content: "哇！写的太好了。",
    replies: [
      {
        id: 2,
        user: "陌上花开",
        avatar: face,
        time: "2 小时前",
        content: "赞！",
      },
      {
        id: 2,
        user: "月水浮华",
        avatar: face,
        time: "2 小时前",
        content: "赞!",
      }
    ]
  }
]);

const constructNewComment = (content) => {
  return {
    id: rid.value++,
    user: "Clors",
    avatar: face,
    content,
    time: "刚刚",
  }
}

const addNewCommend = (content) => {
  const newComment = constructNewComment(content);
  comments.value.push(newComment);
}

const addReply = (content, id) => {
  const reply = constructNewComment(content);
  let comment = comments.value.find((comment) => {
    return comment.id === id;
  })
  if(comment.replies) {
    comment.replies.push(reply);
  }else {
    comment.replies = [reply];
  }
}
</script>

<style>

</style>