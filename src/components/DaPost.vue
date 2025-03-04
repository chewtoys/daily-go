<template>
  <div
    class="card"
    :class="cls">
    <a
      :href="link"
      target="_blank"
      class="post-link vertical"
      @click="onClick">
      <div class="card-background">
        <AsyncImg
          :src="img"
          :placeholder="placeholder"
          sizing="cover"/>
      </div>
      <div class="card-content vertical">
        <div class="card-content-background"/>
        <h3 class="text">{{ title | cardTitle }}</h3>
      </div>
    </a>
    <div class="card-footer horizontal align-center">
      <AsyncImg
        class="logo"
        :src="logo"
        :alt="source"
        sizing="contain"/>
      <h4 class="caption">// {{ source }}</h4>
      <div class="flex"/>
      <button
        class="bookmark"
        @click.prevent="onBookmark">
        <svgicon name="bookmark"/>
      </button>
    </div>
  </div>
</template>

<script>
import AsyncImg from './AsyncImg.vue';

export default {
  name: 'DaPost',

  components: {
    AsyncImg,
  },

  props: {
    postId: {
      type: String,
      required: true,
    },
    link: {
      type: String,
      required: true,
    },
    img: {
      type: String,
      required: true,
    },
    title: {
      type: String,
      required: true,
    },
    source: {
      type: String,
      required: true,
    },
    logo: {
      type: String,
      required: true,
    },
    placeholder: {
      type: String,
      required: true,
    },
    size: {
      type: String,
      default: 'medium',
    },
    bookmarked: {
      type: Boolean,
      default: false,
    },
  },

  methods: {
    onClick() {
      ga('send', 'event', 'Post', 'Click', this.source);
    },

    onBookmark() {
      ga('send', 'event', 'Post', 'Bookmark', this.bookmarked ? 'Remove' : 'Add');
      this.$emit('toggle-bookmark', this.postId);
    },
  },

  computed: {
    cls() {
      return {
        [this.size]: true,
        bookmarked: this.bookmarked,
      };
    },
  },

  mounted() {
    import('../icons/bookmark');
  },
};
</script>

<style scoped>
.logo {
  width: 20px;
  height: 20px;
  margin-right: var(--size-space);
  border-radius: calc(var(--size-space) / 2);
}

.bookmark {
  & .svg-icon {
    color: var(--color-secondary);
  }

  &:hover .svg-icon {
    color: var(--color-primary);
  }

  &:focus {
    outline: 0;
  }
}

.bookmarked .bookmark .svg-icon {
  color: var(--color-highlight);
}

button {
  padding: 0;
  border: none;
  background: none;
}
</style>
