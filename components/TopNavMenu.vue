<script setup>
const route = useRoute();
const props = defineProps(['posts']);
const posts = props.posts.filter((e) => e.category.includes('menu'));
const pathArr = posts.map((e) => e._path.slice(1));

import { selectedClass, borderClasses } from '../utils/selectedHack';
</script>

<template>
  <div id="menu" class="w-full my-4 md:w-fit md:mb-0 md:mt-4">
    <ul class="justify-end p-0 md:flex max-md:mb-0">
      <li
        v-for="(post, index) in posts"
        :key="post._path"
        :class="[
          selectedClass(route, post) ? 'selected' : null,
          borderClasses(route, pathArr, index)
            ? 'md:!border-r-0 md:!border-b !border-b-0'
            : null,
        ]"
      >
        <NuxtLink
          v-if="post._path !== '/words' && post._path !== '/reading'"
          :to="{ path: '/', hash: '#' + post._path.slice(1) }"
        >
          {{ post._path === '/hi-im-janne' ? 'About Me' : post.title }}
        </NuxtLink>
        <NuxtLink v-if="post._path === '/words'" to="/words">{{
          post.title
        }}</NuxtLink>
      </li>
    </ul>
  </div>
</template>

<style lang="postcss" scoped>
#menu > ul > li {
  @apply block mx-0 p-0 overflow-clip;
  @apply bg-indigo-100/20 dark:bg-indigo-900/30;
  /* borders */
  @apply border-indigo-700 border-b border-x first:border-t last:border-b first:rounded-t last:rounded-b;
  /* @media (min-width: 768px) */
  @apply md:inline-block md:py-1 first:md:ml-0 last:md:mr-0;
  /* resets */
  @apply md:border-0 first:md:rounded-none last:md:rounded-none;
  /* borders */
  @apply md:border-r md:border-t md:border-b first:md:rounded-l first:md:border-l last:md:border-b last:md:rounded-r;
}

#menu > ul > li > a {
  @apply text-center;
  @apply block py-2 hover:no-underline md:inline;
  @apply hover:bg-gradient-to-bl hover:from-orange-100 hover:via-purple-100 hover:to-indigo-100;
  @apply hover:dark:from-orange-900/20 hover:dark:via-purple-900/20 hover:dark:to-indigo-800/60;
  @apply md:py-2 md:px-[0.5rem] lg:px-3;
}
.selected {
  @apply bg-gradient-to-tl from-orange-100/50 via-rose-100/50 to-pink-200/50 !border-pink-700 md:!border-l border-t;
  @apply dark:from-orange-900/20 dark:via-rose-900/20 dark:to-pink-800/20;
  a {
    @apply text-pink-500;
    @apply hover:bg-gradient-to-bl hover:from-orange-100 hover:via-rose-100 hover:to-pink-100;
    @apply hover:dark:from-orange-900/10 hover:dark:via-rose-900/20 hover:dark:to-pink-800/20;
  }
}

ul > li:before {
  @apply content-none;
}
</style>
