<template>
  <div id="app">
    <section v-if="loginAcess && !signUp">
        <h2>SIR - ManageMent</h2>
        <table>
                <tr>
                    <th>닉네임</th>
                    <th>닉네임</th>
                    <th>닉네임</th>
                    <th>닉네임</th>
                </tr>
                <tr>
                    <td>테스트</td>
                    <td>테스트</td>
                    <td>테스트</td>
                    <td>테스트</td>
                </tr>
                <tr>
                    <td>테스트</td>
                    <td>테스트</td>
                    <td>테스트</td>
                    <td>테스트</td>
                </tr>
        </table>
    </section>
    <section v-if="!loginAcess && !signUp">
        <div class="box">
          <h1>SIR 동맹관리시스템</h1>
          <input type="text" placeholder="아이디(닉네임)" v-model="userId">
          <input type="password" placeholder="비밀번호" v-model="userPw" @keyup.enter="singIn">
          <input type="button" value="로그인" @click="signIn">
          <input type="button" value="회원가입" @click="signUp=true;">
        </div>
    </section>
    <section v-if="signUp">
        <div class="box">
            <h1>회원가입</h1>
                <input type="text" placeholder="아이디(닉네임)" v-model="userId">
                <input type="password" placeholder="비밀번호" v-model="userPw">
                <input type="password" placeholder="비밀번호확인" v-model="userPwCheck" @keyup.enter="setNewAccount">
                <input type="button" value="가입신청" @click="setNewAccount">
            </div>
        </section>
    </div>
</template>

<script>

export default {
  data () {
    return {
        loginAcess : false,
        userId : '',
        userPw : '',
        userPwCheck: '',
        errorMsg : '',
        signUp : false,
        selectDay : {

        },
    }
  },
  components:{
  },
  methods:{
    signIn(){
        var self = this;
        var params = {
            USER_ID : self.userId,
            USER_PW : self.userPw
        }
        this.axios.post("/api/login",params).then(function(response){
            if(response.data.length>0) {
                if(response.data[0].ALLOW == 1) {
                    self.loginAcess = true;
                }
                else {
                    alert('관리자 승인이 필요한 계정입니다. 관리자에게 문의해주세요.');
                }
            }
            else{
                alert('해당 아이디나 비밀번호가 일치하는 계정이 없습니다.');
            }
        });
    },
    setNewAccount(){
        var self = this;
        if(this.userPw   == this.userPwCheck){
            var params = {
                USER_ID : self.userId,
                USER_PW : self.userPw
            }
            this.axios.post("/api/signup",params).then(function(response){
                alert(response.data.message);
                self.signUp = false;
            });
        }
        else{
            alert('비밀번호 확인을 정확히 입력해주세요.');
        }
    }
  }
}
</script>

<style>
h3.input[type="button"]{
    background-color: white;
    padding: 15px 30px;
    text-align:
    center;font-size: 40px;
    margin: 10px 10px;
    cursor: pointer;
    border-radius: 15px;
    width:600px;
}

.box{
  height: 70%;
  width: 80%;
  position: absolute;
  left: 10%;
  top: 30%;
  background: #191919;
  text-align: center;
}
.box h1{
  color: white;
  text-transform: uppercase;
  font-weight: 500;
}
.box input[type = "text"],.box input[type = "password"]{
  border:0;
  background: none;
  display: block;
  margin: 20px auto;
  text-align: center;
  border: 2px solid #3498db;
  padding: 14px 10px;
  width: 200px;
  outline: none;
  color: white;
  border-radius: 24px;
  transition: 0.25s;
}
.box input[type = "text"]:focus,.box input[type = "password"]:focus{
  border-color: #2ecc71;
}
.box input[type = "button"]{
  border:0;
  background: none;
  display: block;
  margin: 20px auto;
  text-align: center;
  border: 2px solid #2ecc71;
  padding: 14px 40px;
  outline: none;
  color: white;
  border-radius: 24px;
  transition: 0.25s;
  cursor: pointer;
}
.box input[type = "button"]:hover{
  background: #2ecc71;
}

* {
  box-sizing: border-box;
}

html.open, body.open {
  height: 100%;
  overflow: hidden;
}

html {
  padding: 40px;
  font-size: 62.5%;
}

body {
  margin: 0;
  padding: 0;
  font-family: sans-serif;
  background: #191919;
  padding: 20px;
  line-height: 1.6;
  -webkit-font-smoothing: antialiased;
  color: #fff;
}

p {
  text-align: center;
  margin: 20px 0 60px;
}

main {
  background-color: #2C3845;
}

h1 {
  text-align: center;
  font-weight: 300;
}

[type="checkbox"]:checked + label span:last-child {
  background: var(--green);
}

[type="checkbox"]:checked + label span:last-child::before {
  transform: translateX(24px);
}

[type="checkbox"]:checked + label span:last-child::after {
  width: 14px;
  height: 14px;
  /*right: auto;*/
  left: 8px;
  background-image: url(https://s3-us-west-2.amazonaws.com/s.cdpn.io/162656/checkmark-switcher.svg);
  background-size: 14px 14px;
}

</style>
