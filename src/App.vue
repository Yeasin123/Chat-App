<template>
  <section class="main">
    <div class="page-content page-container" id="page-content">
      <div class="padding">
        <div class="row container d-flex justify-content-center">
          <div class="col-md-6 offset-md-3">
            <div class="card card-bordered">
              <div class="card-header">
                <h4 class="card-title">
                  <img
                    class="avatar"
                    src="https://img.icons8.com/color/36/000000/administrator-male.png"
                    alt="..."
                  />Md Yeasin Hossain Imran
                </h4>
              </div>
              <div class="ps-container ps-theme-default ps-active-y" id="chat-content"
                style="overflow-y: scroll !important; height: 400px !important"
              >
                <div class="row">
                    <div class="col-md-12" v-for="(message, index) in allMessages" :key="index">
                    <div class="media media-chat test">
                      <div class="media-body">
                        <p v-if="message.msg">
                          <span>{{ message.msg }}</span>
                        </p>
                         <img v-if="message.image" :src="message.image" width="100" class="uploading-image mt-2" />
                      </div>

                      <div class="media media-chat media-chat-reverse" v-for="(replyMessage, index) in replyMessages" :key="index">
                      <div class="media-body">
                        <p v-if="replyMessage.message_id == message.id">{{replyMessage.reply}} </p>
                      </div>
                    </div>
                    </div>
                  </div>
                </div>
              </div>
              <div class="publisher bt-1 border-light">
                <label for="file-upload" class="custom-file-upload">
                    <i class="fa fa-plus"></i>
                </label>
               <input type="file" accept="image/*" id="file-upload" @change="uploadImage" />
                <input
                  class="publisher-input"
                  type="text"
                  placeholder="Write a message"
                  v-model.trim="chatMessage.textMessage"
                />
                <a
                  class="publisher-btn text-info"
                  href="#"
                  data-abc="true"
                  @click="sendMessage"
                  ><i class="fa fa-paper-plane"></i
                ></a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>

export default {
  name: "App",
  data() {
    return {
      allMessages: [],
      chatMessage: {
        textMessage: '',
        imageMessage: '',
        time:''
      },
      replyMessages:[],
      sentences: [
        "So fat not even Dora can explore her",
        "Fat I swerved to miss her and ran out of gas",
        "Smelly she put on Right Guard and it went left",
        "So fat she hasn’t got cellulite, she’s got celluheavy",
        "So fat she don’t need no internet – she’s already world wide",
        "So hair her armpits look like Don King in a headlock",
        "So classless she could be a Marxist utopia",
        "So fat she can hear bacon cooking in Canada",
        "So fat she won “The Bachelor” because she all those other bitches",
        "So stupid she believes everything that Brian Williams says",
        "So ugly she scared off Flavor Flav",
        "Is like Domino’s Pizza, one call does it all",
        "Twice the man you are",
        "Is like Bazooka Joe, 5 cents a blow",
        "Is like an ATM, open 24/7",
        "Is like a championship ring, everybody puts a finger in her"
      ],
    };
  },
  methods: {
    sendMessage() {
      const id = Date.now()
      if (this.chatMessage.textMessage != "" || this.chatMessage.imageMessage != "") {
          const msg = {
            id:id,
            msg:this.chatMessage.textMessage,
            image:this.chatMessage.imageMessage
          }
          this.allMessages.push(msg)
          this.chatMessage.textMessage=''
          this.chatMessage.imageMessage = '',
        
          this.getRandomSentence(msg.id)
      } else {
        alert("Please Write something");
      }
    },

    getRandomSentence(msg_id) {
         const id = Date.now()
         const index = Math.floor(Math.random() * this.sentences.length);
         const reply = {
          id:id,
          reply:this.sentences[index],
          message_id:msg_id
        }
         this.replyMessages.push(reply)
    },
     uploadImage(e){
        const image = e.target.files[0];
        const reader = new FileReader();
        reader.readAsDataURL(image);
        reader.onload = e =>{
            this.chatMessage.imageMessage = e.target.result;
        };
          
    },
  },

};
</script>
