<template>
  <section>
    <ul>
      <li v-for="post in posts" :key="post.slug" class="h-feed">
        <nuxt-link :to="post.path">
          <div class="meta">
            <h2 class="title p-name" v-text="post.title" />
            <time class="date dt-published" :datetime="post.publishedAt">
              <a :href="fullPath(post.path)" class="u-url">
                {{ post.publishedAt | date }}
              </a>
            </time>
          </div>
          <div class="icon">
            <icons-arrow />
          </div>
        </nuxt-link>
      </li>
    </ul>
    <base-footnote>
      Check out the <a :href="globals.blogFeedURL">RSS feed</a> or
      <a :href="globals.twitterURL">my Twitter account</a>
      to keep up to date.
    </base-footnote>
  </section>
</template>

<script>
import IconsArrow from '@/components/Icons/IconsArrow'

export default {
  name: 'PostsOverview',
  components: { IconsArrow },
  props: {
    posts: {
      type: Array,
      required: true,
    },
  },
  methods: {
    fullPath(path) {
      return `${this.globals.baseURL}${path}`
    },
  },
}
</script>

<style lang="sass" scoped>
ul
  display: flex
  flex-direction: column
  flex-wrap: nowrap
  justify-content: flex-start
  align-content: space-between
  align-items: stretch
li
  > a
    display: flex
    flex-direction: row
    flex-wrap: nowrap
    justify-content: space-between
    align-content: flex-start
    align-items: center
    text-decoration: none
    color: $color-primary
    transition: $animation
    border-radius: $border-radius
    padding: 2rem
    @media (prefers-color-scheme: dark)
      color: $color-light
      &:hover
        color: $color-primary
    @media screen and (max-width: $breakpoint-mobile)
      flex-direction: column
      justify-content: flex-start
      align-items: flex-start
    &:hover
      background: $color-secondary
      .icon
        background: $color-light
        svg
          fill: $color-primary
      .date
        a
          color: $color-primary
      @media (prefers-color-scheme: dark)
        .icon
          background: $color-primary
          svg
            fill: $color-secondary
    .icon
      display: flex
      flex-direction: row
      flex-wrap: nowrap
      justify-content: center
      align-content: center
      align-items: center
      background: $color-secondary
      border-radius: 50%
      font-size: 1.5rem
      line-height: 1.5rem
      padding: .5rem
      margin:  0 0 0 1rem
      transition: $animation
      @media screen and (max-width: $breakpoint-mobile)
        display: none
      svg
        fill: $color-primary
        width: 2rem
        height: 2rem
    .title
      font-size: 1.5rem
    .date
      font-size: 1rem
      @media screen and (max-width: $breakpoint-mobile)
        margin: .5rem 0 0 0
      a
        color: $color-primary
        text-decoration: none
        transition: $animation
        border-bottom: 2px solid transparent
        &:hover
          border-color: $color-primary
        @media (prefers-color-scheme: dark)
          color: $color-light
</style>
