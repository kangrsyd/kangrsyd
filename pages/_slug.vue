<template>
  <div
    class="min-h-screen bg-gray-900 flex flex-col justify-center relative overflow-hidden lg:py-12"
  >
    <div class="absolute inset-0"></div>
    <div
      class="relative w-full font-sans px-6 py-6 bg-gray-900 lg:bg-gray-800 md:max-w-3xl md:mx-auto lg:max-w-4xl lg:pt-16 lg:pb-28"
    >
      <article class="mt-8 prose prose-invert mx-auto lg:prose-lg">
        <NuxtContent :document="page" />
      </article>
    </div>
  </div>
</template>

<script>
export default {
  async asyncData({ $content, params, error }) {
    const slug = params.slug || "index";
    const page = await $content(slug)
      .fetch()
      .catch((err) => {
        error({ statusCode: 404, message: "Page not found" });
      });
    return {
      page,
    };
  },
};
</script>
