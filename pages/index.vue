<template>
  <div>
    <div v-for="(post, index) in posts" :key="index">
      <p>{{ post.short }}</p>
      <nuxt-link :to="post.path">LINK</nuxt-link>
    </div>
  </div>
</template>

<script>
export default {
  name: "BlogOverview",
  auth: false,
  async asyncData({ $content, app, error }) {
    const posts = await $content("blog")
      .only(["short", "path"])
      .sortBy("createdAt", "asc")
      .fetch()
      .catch(() => {
        error({ statusCode: 404, message: "Page not found" });
      });
    return { posts };
  },
};
</script>