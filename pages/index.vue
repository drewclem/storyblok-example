<template>
  <StoryblokComponent v-if="story" :blok="story.content" />
</template>

<script>
import { useStoryblokBridge, useStoryblokApi } from "@storyblok/nuxt-2";

export default {
  asyncData: async ({ app }) => {
    const storyblokApi = useStoryblokApi();
    const { data } = await storyblokApi.get("cdn/stories/home", {
      version: "draft",
    });

    return { story: data.story };
  },
  mounted() {
    useStoryblokBridge(this.story.id, (newStory) => (this.story = newStory));
  },
};
</script>
