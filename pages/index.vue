<script setup>
const props = defineProps(['posts']);
const pattern = [
  '3',
  '3',
  '4',
  '2',
  '2',
  '4',
  '3',
  '3',
  '2',
  '2',
  '2',
  '3',
  '3',
  '6',
  '2',
  '4',
];

const posts = props.posts.filter((e) => e.category.includes('index'));

function getWidth(index) {
  return pattern[index % 16];
}
</script>

<template>
  <main>
    <div class="content-grid">
      <ContentCard
        v-for="(post, index) in posts"
        :key="post._path"
        :post="post"
        :class="[
          getWidth(index) === '2'
            ? 'col-span-2'
            : getWidth(index) === '4'
            ? 'col-span-4'
            : getWidth(index) === '6'
            ? 'col-span-6'
            : 'col-span-3',
        ]"
      >
        <ContentRenderer :value="post">
          <ContentText :class="post._path.slice(1) + '-text'">
            <h2 :id="post._path.slice(1)">
              <NuxtLink :to="{ path: '/', hash: '#' + post._path.slice(1) }">
                {{ post.title }}
              </NuxtLink>
            </h2>
            <ContentRendererMarkdown :value="post" />
          </ContentText>
        </ContentRenderer>
        <ContentMeta v-if="post.meta" :post="post" />
      </ContentCard>
    </div>
  </main>
</template>

<style lang="postcss" scoped>
.contact-text {
  :deep(li:before) {
    content: none;
  }
}
</style>
