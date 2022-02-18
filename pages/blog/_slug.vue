<template>
  <div>
    <h1>{{ post.title }}</h1>
    <nuxt-content :document="post" />
    <nuxt-link to="/">Index</nuxt-link>
  </div>
</template>

<script>
export default {
  name: "BlogSlug",
  auth: false,
  async asyncData({ $content, params, app, error }) {
    const post = await $content("blog", params.slug)
      .fetch()
      .catch(() => {
        error({ statusCode: 404, message: "Page not found" });
      });
    return { post };
  },
};
</script>