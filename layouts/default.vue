<template>
  <b-container>
    <unplugged-header />
    <img
      v-if="$nuxt.$route.name === 'index'"
      src="~/assets/images/main.jpg"
      style="width:100%"
    />
    <b-row>
      <b-col>
        <span v-if="room">
          例会教室は<b>{{ room }}</b>
          です.
        </span>
        <span v-if="$nuxt.$route.name !== 'meeting-room'">
          一覧は<a href="https://message.ku-unplugged.net/meeting_room/" target="_blank">こちら</a>
        </span>
      </b-col>
    </b-row>
    <b-row>
      <b-col md="8">
        <nuxt />
      </b-col>
      <b-col md="4">
        <unplugged-sidebar />
      </b-col>
    </b-row>
    <unplugged-footer />
  </b-container>
</template>
<script>
import unpluggedHeader from '~/components/header.vue'
import unpluggedFooter from '~/components/footer.vue'
import unpluggedSidebar from '~/components/sidebar.vue'
import moment from 'moment'

export default {
  components: {
    unpluggedHeader,
    unpluggedFooter,
    unpluggedSidebar
  },
  data: function() {
    return {
      room: ''
    }
  },
  created: function() {
    this.$axios
      .$get('https://message.ku-unplugged.net/api/meeting_room/today/')
      .then(res => {
        this.room = res.room == null ? "終日使用不可" : res.room
      })
  },
  filters: {
    md: function(date) {
      return moment(date).format('MM/DD')
    }
  }
}
</script>
<style>
.container {
  padding: 0px;
}
.row {
  margin: 0px;
}
h1 {
  /* clear: both; */
  margin-top: 15px;
  margin-bottom: 15px;
  padding-left: 35px;
  padding-bottom: 10px;
  border-bottom: 3px dotted #fd9e00;
  background: url('~assets/images/h1-arrow.gif') left top no-repeat;
  color: #463100;
  font-size: 1.6em;
  /* letter-spacing: 0.25em; */
  font-weight: bold;
  font-family: 'ＭＳ Ｐ明朝', serif;
}
h2 {
  clear: both;
  margin: 30px 10px 14px 10px;
  margin-bottom: 14px;
  margin-bottom: 14px;
  padding: 10px 10px 10px 22px;
  background: none;
  border-left: 10px solid #fd9e00;
  border-bottom: 1px solid #ffeeaa;
  font-size: 1.286em;
  font-weight: bold;
  font-family: 'ＭＳ Ｐ明朝', serif;
}
p {
  margin-left: 20px;
  margin-right: 10px;
  margin-bottom: 1rem;
}
a {
  text-decoration: underline;
  color: #463100;
}
a:hover {
  color: #fd9e00;
}
</style>
