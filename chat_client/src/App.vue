<template>
  <div id="app">
      <div class="room-box">
        <div>Nhập id room:</div>
        <div><input type="text" class="in-room" v-model="room.id"></div>
        <div><button @click="subRoomID">Nhập</button></div>
      </div>
      <div class="chat-box">
        <span>Room: {{room.id}}</span>
        <div class="msg-box">
          <div v-for="(item, index) in listMes" 
          :key="index" 
          :class="['msg', item.account == 0? 'self':'friend']" 
          >
            {{item.msg}}
          </div>
        </div>
        <div class="do-chat">
          <input type="text" class="in-text" v-model="mesSend.msg"  @keypress.enter="send()">
          <button class="btn-send" @click="send()" >Send</button>
        </div>
      </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  components: {
  },
  methods: {
    // hàm gửi tin nhắn
    send()
    {
      let me = this;
      me.listMes.push(me.mesSend)
    },

    receive()
    {
      let me = this;
      let mesSocket = '';// gán tin nhắn vào biến này
      //xử lí nhận tin nhắn từ socket


      // dẩy tin nhắn
      me.mesReceive.msg = mesSocket;
      me.listMes.push(me.mesReceive);
    },

    // hàm gọi len server xử lí room id
    subRoomID()
    {
      //biến gửi this.room.id;
    }
    
  },
  data() {
    return {
      // đối tượng phòng
      room:
      {
        id: '',//trường mặc định đừng xóa
        // muốn thêm trường j vào cứ thêm vd (vietanh: true, long: false)
      },

      mesReceive: 
      {
        msg: '',
        account:1,
      },
      mesSend: 
      {
        msg: '',
        account:0,
      },
      // data fake
      listMes: [
        {
          account: 0,
          msg: 'helo minh',
        },
        {
          account: 1,
          msg: "Helo Tho"
        }
      ],
    }
  },
}
</script>

<style>
@import url('./assets/css/main.css');
</style>
