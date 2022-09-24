<template>
  <ul></ul>
</template>

<script>
export default {
  data() {
    return {
      storeResources: [
        {
          id: 'offical guide',
          title: 'Official Guide',
          description: 'The official Vue.js documentation.',
          link: 'https://vuejs.org',
        },
        {
          id: 'google',
          title: 'Google Guide',
          description: 'Learning everything',
          link: 'https://google.com',
        },
      ],
    };
  },
};
</script>
