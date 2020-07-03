<template>
  <div id="inner">
    <Top :event="event" :room="room" />
    <iframe src="https://tokbox.com/embed/embed/ot-embed.js?embedId=3d2c73f1-0a27-4eb1-974e-1ea7c7abcda4&room=DEFAULT_ROOM&iframe=true" scrolling="auto" allow="microphone; camera" ></iframe>
  </div>
</template>

<script>
import Top from '~/components/Top'
export default {
  components: {
    Top
  },
  computed: {
    event () {
      return this.$store.state.events.find(e => e.slug === this.$route.params.event)
    },
    room () {
      return this.event.rooms.find(r => r.slug === this.$route.params.room)
    },
    embedId () {
      return process.env.EMBED_ID
    }
  },
  validate ({ params, store }) {
    const event = store.state.events.find(e => e.slug === params.event)
    return event.rooms.find(r => r.slug === params.room)
  }
}
</script>

<style scoped>
iframe {
  flex: 1;
}
</style>
