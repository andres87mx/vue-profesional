<template lang="pug">
    .container
      .columns
        .column.is-5.is-offset-4
          .notification(:class="notification.type")
            slot(name="body") {{ notification.message }}
</template>
<script>
export default {
  props: {
    notification: { type: Object, required: true }
  }
}
</script>
<style lang="scss">
  .notification {
    margin: 10px;
  }
</style>
