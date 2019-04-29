<template>
  <div class="filter__outer">
    <h1>This is the Filter component.</h1>
  </div>
</template>

<script>
export default {
  name: 'FilterExample',

  data: () => ({
    items: [
      {
        role: 'Admin',
        fascia: 'JDSPORTS',
        services: ['Content Editor'],
      },
      {
        role: 'User',
        fascia: 'JDSPORTS',
        services: ['Content Editor'],
      },
      {
        role: 'Admin',
        fascia: 'JDSPORTS_BE',
        services: ['Content Editor'],
      },
      {
        role: 'User',
        fascia: 'JDSPORTS',
        services: ['Email Builder'],
      },
    ],
  }),
};
</script>
