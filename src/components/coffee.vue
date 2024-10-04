<template>
  <div class="email-form">
    <h2>
      신희성과<br />
      <span class="coffee-chat">☕️ 커피챗을 나눠보세요.</span>
    </h2>
    <form @submit.prevent="sendEmail">
      <label for="name">이름</label>
      <input type="text" id="name" v-model="formData.name" required />

      <label for="email">이메일</label>
      <input type="email" id="email" v-model="formData.email" required />

      <label for="message">메시지</label>
      <textarea id="message" v-model="formData.message" required></textarea>

      <button type="submit">보내기</button>
    </form>
  </div>
</template>

<script>
import emailjs from 'emailjs-com';

export default {
  data() {
    return {
      formData: {
        name: '',
        email: '',
        message: ''
      }
    };
  },
  methods: {
    sendEmail() {
      const serviceID = 'siniseongcoffeechat'; 
      const templateID = 'template_owywfkv'; 
      const publicKey = 'BnijAvwQkU_x2OLRd';

      const templateParams = {
        from_name: this.formData.name,
        from_email: this.formData.email,
        message: this.formData.message,
        to_email: this.formData.email 
      };

      emailjs.send(serviceID, templateID, templateParams, publicKey)
        .then(() => {
          alert('메시지가 성공적으로 전송되었습니다.');
          this.formData.name = '';
          this.formData.email = '';
          this.formData.message = '';
        }, (error) => {
          console.error('Failed to send email:', error);
          alert('메시지 전송에 실패했습니다.');
        });
    }
  }
};
</script>

<style>


h2 {
  font-size: 80px; 
  text-align: left; 
  margin-bottom: 20px; 
  color: #000000;
}

.coffee-chat {
  display: inline-block; 
  text-align: left; 
}

label {
  display: block; 
  margin-top: 20px; 
}

input, textarea, button {
  width: 100%; 
  padding: 10px; 
  margin-top: 10px; 
  box-sizing: border-box; 
}
</style>
