<template>
  <div class="email-form">
    <h2>
      신희성과<br />
      <span class="coffee-chat">☕️ 커피챗</span>을 나눠보세요.
    </h2>
    <form @submit.prevent="sendEmail">
      <div class="input-group">
        <label for="name" :class="{ 'active': formData.name }">이름</label>
        <div class="underline">
          <input type="text" id="name" v-model="formData.name" required />
        </div>
      </div>

      <div class="input-group">
        <label for="email" :class="{ 'active': formData.email }">이메일</label>
        <div class="underline">
          <input type="email" id="email" v-model="formData.email" required />
        </div>
      </div>

      <div class="input-group">
        <label for="message" :class="{ 'active': formData.message }">메시지</label>
        <div class="underline">
          <textarea id="message" v-model="formData.message" required></textarea>
        </div>
      </div>

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
  margin-top: 180px;
  margin-bottom: 20px; 
  color: #000000;
  margin-left: 30px;
}

.coffee-chat {
  display: inline-block; 
  text-align: left; 
  color: #392820; 
}

.input-group {
  position: relative; 
  margin-top: 30px; 
}

label {
  position: absolute; 
  left: 10px; 
  top: -10px; 
  font-size: 16px; 
  color: #999; 
  transition: all 0.2s;
}

label.active {
  font-size: 12px; 
  color: #392820; 
}

.underline {
  border-bottom: 2px solid #ccc; 
  position: relative;
  padding-bottom: 5px; 
}

input, textarea {
  width: 100%; 
  padding: 12px; 
  margin-top: 5px; 
  box-sizing: border-box; 
  border: none; 
  outline: none;
  font-size: 16px; 
  border-radius: 4px; 
  transition: border 0.2s; 
}

input:focus, textarea:focus {
  border-bottom: 2px solid #392820; 
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1); 
}

textarea {
  resize: none; 
  min-height: 100px;
  max-height: 300px; 
}

button {
  width: 100%; 
  padding: 12px; 
  margin-top: 20px; 
  background-color: #392820; 
  color: white; 
  border: none; 
  border-radius: 4px; 
  cursor: pointer; 
  transition: background-color 0.2s; 
}

button:hover {
  background-color: #554545; 
}
</style>
