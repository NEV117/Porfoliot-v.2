<template>
  <div class="exprience-component">
    Exprience Component
  </div>
</template>

<script>
export default {
  name: 'Exprience',  
  setup() {
    const config = useRuntimeConfig()

    return {
      config
    }
  },/* 
  methods: {
    updateLines() {
      const textContainer = this.$el;
      const style = window.getComputedStyle(textContainer);
      const fontSize = parseInt(style.fontSize);
      const lineHeight = parseInt(style.lineHeight);
      const maxHeight = textContainer.offsetHeight;
      this.lines = Math.ceil(maxHeight / lineHeight) + 1;
    }
  }, */
  computed: {
    // Set active class to current page link
    isActive() {
      return route => this.$route.path === route;
    },
  }
};
</script>

<style scoped>
.exprience-component {
  display: flex;
  align-items: flex-start;
}

/* Add other styles here */
</style>
