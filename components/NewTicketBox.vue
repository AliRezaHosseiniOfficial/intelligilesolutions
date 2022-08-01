<template>
  <Modal title="Add New Ticket" :open="open" @close="$emit('close', true)">
    <div class="px-4 py-4 d-flex flex-column justify-content-between align-items-center">
      <select class="form-select form-select-lg form-input">
        <option selected>Related to...</option>
        <option v-for="(item, i) in department" :key="i" :value="item">{{ item }}</option>
      </select>
      <select class="form-select form-select-lg form-input">
        <option selected>Please select your department...</option>
        <option v-for="(item, i) in department" :key="i" :value="item">{{ item }}</option>
      </select>
      <select v-model="selectPriority" class="form-select form-select-lg form-input">
        <option value="noselect" selected>Please select priority...</option>
        <option v-for="(item, i) in priority" :key="i" :value="item">{{ item }}</option>
      </select>
      <input v-model="subject" class="form-control form-input mt-2 mb-4" type="text"
             placeholder="Write your subject...">
      <v-editor v-model="message"/>
      <div @click="sendTicket" class="button-add">Send Ticket</div>
    </div>
  </Modal>
</template>

<script>
import Modal from "@/components/Modal";
import InputField from "@/components/InputField";
import axios from "axios";

export default {
  name: "NewTicketBox",
  components: {InputField, Modal},
  props: ['open'],
  data() {
    return {
      relatedTo: [],
      priority: ['low', 'medium', 'height'],
      department: ['Sale', 'Finance', 'Support'],
      subject: '',
      message: '',
      selectPriority: 'noselect',
    }
  },
  methods: {
    async sendTicket() {
      const config = {
        method: 'post',
        url: "https://api.intelligilesolutions.com/wp-json/wp/v2/ticket",
        headers: {
          "Accept": "application/json",
          "Authorization": "Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwczpcL1wvYXBpLmludGVsbGlnaWxlc29sdXRpb25zLmNvbSIsImlhdCI6MTY1OTI2NDA5MSwibmJmIjoxNjU5MjY0MDkxLCJleHAiOjE2NTk4Njg4OTEsImRhdGEiOnsidXNlciI6eyJpZCI6IjMwIn19fQ.t9rBxmg6RH6uYkSQY7xQsx9QcQdwmKzBfpzmpznev8I"
        },
        data: {
          acf: {
            "ticket_content": this.message,
            "ticket_Priority": this.selectPriority,
            "ticket_subject": "",
            "ticket_author": "TEST",
            "ticket_status": "pending",
            "date": new Date().toDateString(),
            "time": new Date().toTimeString()
          }
        }
      }
      await axios(config).then(res => {
        this.$emit('close', false)
      }).catch(err => {
        console.log(err)
      })
    }
  }
}
</script>

<style scoped>
.button-add {
  display: flex;
  align-items: center;
  height: 40px;
  font-size: 20px;
  color: white;
  background-color: #e99d7b;
  border: none;
  border-radius: 8px;
  padding: 6px 48px;
  transition: all 0.3s ease-in-out;
  cursor: pointer;
  margin-top: 24px;
}

.button-add:hover {
  background-color: #e8926a
}

.form-input {
  border: none;
  background-color: #eff0f4;
  border-radius: 10px;
  margin-bottom: 12px;
  height: 48px;
  font-size: 16px;
}

.form-select {
  display: block;
  width: 100%;
  font-weight: 400;
  line-height: 1.5;
  padding-left: 15px;
  background-image: url('~/assets/svg/selection.svg') !important;
  background-position: right 0.75rem center;
  background-size: 16px 12px;
  transition: border-color .15s ease-in-out, box-shadow .15s ease-in-out;
  appearance: none;
}

.ck.ck-editor {
  width: 100% !important;
}

.ck-editor__editable {
  border: none;
  background-color: #eff0f4 !important;
}

</style>