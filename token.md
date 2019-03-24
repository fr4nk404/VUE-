最近两天写了登录认证的过程，因为用了前后端分离，并且使用OAuth统一登录，所以OAuth请求交互部分集中在后台。这里简单记录一下前台获取token的过程。
```
created() {
          let token = this.$router.currentRoute.query.token;
          if (this.isLoggedin()) {
              // 登录过的用户，跳转到首页
              this.$router.replace('/')
          }
          else if (token) {
              console.log(token)
              this.successLogin(token)
          }
          else {
              window.location.href = "/login/"
          }
      },
      methods: {
          successLogin(token) {
              // 存储 ACCESS_TOKEN 进 localstorage
              window.localStorage.setItem('ACCESS_TOKEN', token);
              Axios.defaults.headers.common['Authorzation'] =
                  'Bearer ' + localStorage.getItem('ACCESS_TOKEN');
          },
          isLoggedin() {
              let token = window.localStorage.getItem("ACCESS_TOKEN");
              if (token) {
                  Axios.defaults.headers.common['Authorization'] =
                      'Bearer ' + token;
                  return true
              } else {
                  return false
              }
          }
      }
```
