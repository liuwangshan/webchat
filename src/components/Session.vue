<template>
  <div class="wc-session" @click="$emit('switch-session', session.from)">
    <mt-cell
    :title="session.remark || session.from"
    :label="session.lastMessage.content"
    >
      <wc-profile-photo :username="session.from" :realName="session.remark">
      </wc-profile-photo>
    </mt-cell>
    <span  class="time">{{ session.lastMessage.timestamp | time }}</span>
    <mt-badge size="small" color="red" v-show="session.unreadMsgCount">
      {{ session.unreadMsgCount > 99 ? '99+' : session.unreadMsgCount}}
    </mt-badge>
  </div>
</template>
<script>
  import {mapGetters} from 'vuex'
  import WcProfilePhoto from "./ProfilePhoto";

  export default {
    name: 'Session',
    components: {WcProfilePhoto},
    props: {
      session: Object,
      active: Boolean
    },
    computed: {
      ...mapGetters({
        friendsInfo: 'friendsInfo'
      }),
      profilePhoto() {
        let info = this.friendsInfo[this.session.from]
        if (info) {
          return info.profilePhoto
        }
        return ''
      }
    }
  }
</script>
<style lang="scss">
  .wc-session {
    position: relative;
    height: 60px;
    .mint-cell {
      .mint-cell-value {
        position: absolute;
        left: 10px;
        top: 7px;
        img {
          border-radius: 5px;
        }
      }
      > .mint-cell-wrapper {
        height: 60px !important;
        .mint-cell-title {
          position: absolute;
          left: 65px;
          height: 45px;
          top: 8px;
          width: 100%;
          .mint-cell-text {
            font-size: 16px;
          }
          .mint-cell-label {
            font-size: 14px;
            margin-top: 9px;
            overflow: hidden;
            text-overflow: ellipsis;
            white-space: nowrap;
            width: 80%;
          }
        }
      }
    }
    .time {
      position: absolute;
      right: 10px;
      top: 10px;
      font-size: 14px;
      color: #888;
    }
    .mint-badge {
      position: absolute;
      top: 2px;
      left: 45px;
    }
  }

</style>
