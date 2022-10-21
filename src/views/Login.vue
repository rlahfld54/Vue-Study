<template>
  <div>
    <h1>Login</h1>
    <form v-on:submit.prevent="submitForm">
      <div>
        <label for="username">id:</label>
        <input id="username" type="text" v-model="username">
      </div>
      <div>
        <label for="password">pw:</label>
        <input id="password" type="password" v-model="password">
      </div>
      <button type="submit">login</button>
      <!-- <button type="button" @click="checkInfo">정보확인</button> -->
    </form>
  </div>
</template>
  
<script>
export default {
  data() {
    return {
      username: '',
      password: '',
      tempString : null
    }
  },
  methods: {
    submitForm() {
      var url = 'https://jsonplaceholder.typicode.com/users';
      const person = {
        username: this.username,
        password: parseInt(this.password)
      }
      // console.log(this.username, this.password);
      // 서버에서 정보를 가져올땐 get()
      // console.log(this)
      var vm = this

      this.axios.get(url)
      .then(function (response) {

          console.log(vm)

          // 내가 짠 코드
          response.data.find((element, idx) => {
            console.log(element)
            if (element.username == person.username && element.id == person.password) {

              console.log("Work!!!!!!!!@#@@#");
              return true

              // 메인 페이지로 이동!!
              // this.$router.push('/home')
            } else if (element.username == person.username && element.id !== person.password){

              console.log("비밀번호가 틀렸습니다.");
              return true

              
            } else if (element.username !== person.username && element.id == person.password){

              console.log("아이디가 틀렸습니다.");
              return true

            } 
            else {
              if(idx === response.data.length-1){
                console.log("없는 사용자입니다.");
                return true
              }
            }

            if(element.username == person.username){
              if(element.id == person.password){
                console.log('성공')
                return true
              }else{
                console.log('패스워드 오류')
                return true
              }
            }else{
              if(idx === response.data.length-1){
                console.log('없는 사용자')
                return true
              }
            }
          });

          // 종훈씨가 짠 코드
          // response.data.some((ele, idx) => {
          //   if(ele.username == person.username){
          //     if(ele.id == person.password){
          //       console.log('성공')
          //       return true
          //     }else{
          //       console.log('패스워드 오류')
          //       return true
          //     }
          //   }
          //   else{
          //     if(idx === response.data.length-1){
          //       console.log('없는 사용자')
          //       return true
          //     }
          //   }
          // })


        })

    },
    checkInfo() {
      this.$router.push('/home')
    }
  }
}
</script>