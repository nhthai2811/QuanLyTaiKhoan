<template>
  <div>
    <md-app>
      <md-app-drawer md-permanent="full">
        <md-list class="menu">
          <md-list-item>
            <NuxtLink to="/">
              <md-button md-menu-trigger class="btmenu">Quản lý tài khoản</md-button>
            </NuxtLink>
          </md-list-item>
          <md-list-item>
              <md-button md-menu-trigger @click="showDialog = true" class="btmenu">Tạo tài khoản</md-button>
          </md-list-item>
        </md-list>
      </md-app-drawer>

      <md-app-content>
        <div v-if="viewmode === 'list'">
          <md-button class="md-dense md-raised md-mini md-fab-bottom-right md-primary" @click="viewmode = 'list'">List</md-button>
          <md-button class="md-dense md-raised md-mini md-fab-bottom-right" @click="viewmode = 'card'">Card</md-button>
        </div>
        <div v-if="viewmode === 'card'">
          <md-button class="md-dense md-raised md-mini" @click="viewmode = 'list'">List</md-button>
          <md-button class="md-dense md-raised md-mini md-primary" @click="viewmode = 'card'">Card</md-button>
        </div>
        <div id="listAccount">
          <div v-for="account in accounts" :key="account._id" class="md-elevation-2 info-box">
              <div v-if="viewmode === 'card'" class="md-card md-with-hover">
                <md-card-header>
                  <md-card-header-text>
                    <span>{{account.name}}</span><br>
                    <span>{{account.username}}</span>
                    <span>{{account.email}}</span><br>
                    <span>{{account.address}}</span>
                    <span>{{account.date}}</span>
                  </md-card-header-text>

                  <md-card-media>
                    <img :src="account.avt" alt="Avatar">
                  </md-card-media>
                </md-card-header>

                <div class="md-card-actions">
                  <md-button md-menu-trigger v-on:click="editModal(account.id)">Sửa</md-button>
                  <md-button class="md-accent" v-on:click="delModal(account.id)">Xóa</md-button>
                </div>
              </div>
              <div v-if="viewmode === 'list'" class="md-list md-list-hover">
                <md-list-item>
                  <md-avatar>
                    <img class="avt" :src="account.avt" alt="People">
                  </md-avatar>
                  <div class="md-list-item-text">
                    <span>{{account.username}}</span>
                    <span>{{account.name}}</span>
                    <span>{{account.date}}</span>
                    <span>{{account.email}}</span>
                  </div>
                  <md-button md-menu-trigger v-on:click="editModal(account.id)">Sửa</md-button>
                  <md-button class="md-accent" v-on:click="delModal(account.id)">Xóa</md-button>
                </md-list-item>
              </div>
          </div> 
        </div>
      </md-app-content>
    </md-app>
    <div>
      <md-dialog :md-active.sync="showDialog">
        <md-dialog-title>Thêm</md-dialog-title>

        <form class="createForm" id="create" name="createForm" v-on:submit.prevent="onSubmit()">
            <md-field class="md-field-dialog" :md-counter="false">
              <label>Tên tài khoản</label>
              <md-input v-model="naccount.username" name="username" maxlength="8" ></md-input>
            </md-field>
            <div class="error" v-if="errors.username">{{errors.username}}</div>
            <md-field class="md-field-dialog" :md-counter="false">
              <label>Họ và tên</label>
              <md-input v-model="naccount.name" name="name" maxlength="20"></md-input>
            </md-field>
            <md-field class="md-field-dialog">
              <label>Email</label>
              <md-input v-model="naccount.email" name="email" type="email" ></md-input>
            </md-field>
            <div class="error" v-if="errors.email">{{errors.email}}</div>
            <div class="md-field-dialog">
              <md-datepicker v-model="naccount.date" >
              <label>Ngày sinh</label>
              </md-datepicker>
            </div>
            <div class="error" v-if="errors.date">{{errors.date}}</div>
            <div class="md-field-dialog">
              <div>
                <md-radio v-model="naccount.gender" value="nam" class="md-primary">Nam</md-radio>
                <md-radio v-model="naccount.gender" value="nu" class="md-primary">Nữ</md-radio>
              </div>
            </div>
            <div class="error" v-if="errors.gender">{{errors.gender}}</div>
            <md-field class="md-field-dialog" :md-counter="false">
              <label>Địa chỉ</label>
              <md-textarea v-model="naccount.address" maxlength="200" md-autogrow ></md-textarea>
            </md-field>
            <div class="error" v-if="errors.address">{{errors.address}}</div>
            <md-card-actions class="btmodal">
              <md-button type="submit" class="md-primary">Tạo tài khoản</md-button>
              <md-button class="md-primary" @click="showDialog = false">Close</md-button>
            </md-card-actions>
          </form>
      </md-dialog>
    </div>

    <div>
      <md-dialog :md-active.sync="showDialogEdit">
        <md-dialog-title>Sửa</md-dialog-title>

        <form class="createForm" id="create">
            <md-field class="md-field-dialog">
              <label>Tên tài khoản</label>
              <md-input v-model="editAccount.username" name="username" maxlength="8"></md-input>
            </md-field>
            <md-field class="md-field-dialog">
              <label>Họ và tên</label>
              <md-input v-model="editAccount.name" name="name"></md-input>
            </md-field>
            <md-field class="md-field-dialog">
              <label>Email</label>
              <md-input v-model="editAccount.email" name="email"></md-input>
            </md-field>
            <div class="md-field-dialog">
              <md-datepicker v-model="editAccount.date">
              <label>Ngày sinh</label>
              </md-datepicker>
            </div>
            
            <div class="md-field-dialog">
              <div>
                <md-radio v-model="editAccount.gender" value="nam" class="md-primary">Nam</md-radio>
                <md-radio v-model="editAccount.gender" value="nu" class="md-primary">Nữ</md-radio>
              </div>
            </div>
            <md-card-actions class="btmodal">
              <md-button type="submit" class="md-primary"  @click.prevent="onSave">Tạo tài khoản</md-button>
              <md-button class="md-primary" @click="showDialogEdit = false">Close</md-button>
            </md-card-actions>
          </form>
      </md-dialog>
    </div>
  </div>
</template>

<style lang="css" scoped>

.md-list-hover:hover {
    cursor: pointer;
    box-shadow: 0 5px 15px 2px rgba(3, 5, 5, 0.1);
    transition-duration: 0.3s, 0.4s;
}

.page-container {
  margin: 0px;
}

.md-app-drawer, .menu  {
  background-color:  #448aff;
}

.menu {
  margin-top: 30px;
}

.btmodal{
  margin-bottom: 30px;
}

.btmenu {
  color: #fff;
  margin: 10px;
}

.md-card {
    width: 320px;
    margin: 4px;
    display: inline-block;
    vertical-align: top;
    float: left;
  }
.info-box{
    list-style-position:inside;
    margin: 10px;
}
  .list {
    list-style: none;
  }

  .md-switch {
    display: flex;
  }

  .page-container {
    margin: 10px;
  }

  #search-input {
    height: 50px;
  }
  .md-app {
    height: 1080px;
    border: 1px solid rgba(#000, .12);
  }

  .md-field {
    max-height: 200px;
    border: 1px solid rgba(#fff, .12);
    background: #fff;
  }

  .md-drawer {
    width: 230px;
    max-width: calc(100vw - 125px);
  }

  .md-radio {
    display: flex;
  }

   .createForm {
    max-width: 600px;
  }

  .md-field-dialog {
    max-height: 200px;
    border: 1px solid rgba(#fff, .12);
    background: #fff;
    margin: 10px 10px 10px 60px;
  }
  .md-dialog-container .md-theme-default  {
    width: 450px;
  }

  .error {
    color: red;
    font-size: 75%;
    margin-left: 10%;
  }
</style>

<script>
import format from 'date-fns/format'
import Vue from 'vue'
import VueMaterial from 'vue-material'
import 'vue-material/dist/vue-material.min.css'
import 'vue-material/dist/theme/default.css'
import Vuelidate from 'vuelidate'
import { required, email, minLength, maxLength } from 'vuelidate/lib/validators'

Vue.use(VueMaterial);
Vue.use(Vuelidate);
// let account = [
//         {
//           id: 1,
//           avt: 'https://st3.depositphotos.com/1767687/16607/v/450/depositphotos_166074422-stock-illustration-default-avatar-profile-icon-grey.jpg',
//           username: 'nhthai12',
//           name: 'Nguyen Hoang Thai',
//           date: '0343579108',
//           email: 'hoangthai123@gmail.com',
//           gender: 'nam',
//         },
//         {
//           id: 2,
//           avt: 'https://st3.depositphotos.com/1767687/16607/v/450/depositphotos_166074422-stock-illustration-default-avatar-profile-icon-grey.jpg',
//           username: 'nhthong1',
//           name: 'Nguyen Hoang Thong',
//           date: '0903456471',
//           email: 'hoangthong123@gmail.com',
//           gender: 'nam',
//         },
//         {
//           id: 3,
//           avt: 'https://www.smiledental.co.nz/wp-content/uploads/1997/12/generic-avatar-female-2-300x300.png',
//           username: 'nhphu123',
//           name: 'Nguyen Hoang Phu',
//           date: '0121568423',
//           email: 'hoangphu123@gmail.com',
//           gender: 'nu',
//         },
//       ]
// account = JSON.stringify(account);
// if (process.browser) {
//   window.localStorage.setItem('account', account);
// }

  // if (process.browser) {
  //  let accounts1 =  window.localStorage.getItem('account');
  // //  account1 = JSON.parseJson(accounts1);
  //  console.log(accounts1);
  // }
  
import $ from 'jquery';  

export default {
  name: 'RegularSwitch',
  // props: {
  //   account: {
  //     type: Object,
  //     default: {
  //       name: '',
  //       username: '',
  //       pw: '',
  //       cpw: '',
  //       address: '',
  //       date: '',
  //     }
  //   }
  // },

  data() {
      return {
      accounts: [
      ],
      naccount: [{
      }],
      editAccount: [{
        name: '',
        email: '',
        pw: '',
        cpw: '',
        date: '',
        address: '',
      }],     
      errors: [{
        username: '',
        name: '',
        date: '',
        address: '',
        gmail: '',
        gender: '',
      }],
      switchs: 0,
      radio: 'accent',
      viewmode: 'list',
      showDialog: false,
      showDialogEdit: false,
      isSubmit: false,
      editButton: false,
      selectedDate: null,
      gender: null,
      del: false,
      check: null,

      //   editAccount: this.account ? {...this.account } : {
      //   name: '',
      //   username: '',
      //   pw: '',
      //   cpw: '',
      //   address: '',
      //   date: '',
      // }
    }
  },

  created() {
    if(process.browser) {
      let data = localStorage.getItem('account');
      data = JSON.parse(data);
      this.accounts = data;
      // $( "#listAccount" ).sortable();
    }
  },

 
  methods:{

    validate()
    {
      this.errors = [{
        username: '',
        name: '',
        date: '',
        address: '',
        gmail: '',
        gender: '',
      }];
      let isValid = true;
      if (!this.naccount.username) {
        this.errors.username = "Bạn cần nhập tên tài khoản.";
        isValid = false;
      }
      // const nameRegex = /^[a-zA-Z0-9]+$/;
      // let checkusername = this.naccount.username.match(nameRegex);
      // if (checkusername == null) {
      //   this.errors.username = "Tên tài khoản không đúng quy định.";
      //   isValid = false;
      // }
      if (!this.naccount.date) {
        this.errors.date = "Bạn cần chọn ngày sinh.";
        isValid = false;
      }
      if (!this.naccount.gender) {
        this.errors.gender = "Bạn cần chọn giới tính.";
        isValid = false;
      }
      if (!this.naccount.address) {
        this.errors.address = "Bạn cần nhập địa chỉ.";
        isValid = false;
      }
      if (!this.naccount.email) {
        this.errors.email = "Bạn cần nhập email.";
        isValid = false;
      }
      return isValid;
    },

    onSubmit(){
      if (this.validate()) {
        this.showDialog = false;
          if (process.browser) {
            let data = localStorage.getItem('account');
            data = JSON.parse(data);
            if(!data){
              data = [];
            }
            let id = data.length + 1;
            let account = 
            {
              id: id,
              avt: 'avtboy.jpg',
              username: this.naccount.username,
              name: this.naccount.name,
              date: format(this.naccount.date, "yyyy-MM-dd"),
              email: this.naccount.email,
              gender: this.naccount.gender,
            };
            if(account.gender == 'nu') account.avt = 'avtgirl.jpg' ;
            data.push(account);
            data = JSON.stringify(data);
            window.localStorage.setItem('account', data);
            window.location.reload();
          }
      }
      // this.showDialog = false;
      // if (process.browser) {
      //   let data = localStorage.getItem('account');
      //   data = JSON.parse(data);
      //   if(!data){
      //     data = [];
      //   }
      //   let id = data.length + 1;
      //   let account = 
      //   {
      //     id: id,
      //     avt: '/_nuxt/assets/avtboy.jpg',
      //     username: this.naccount.username,
      //     name: this.naccount.name,
      //     date: format(this.naccount.date, "yyyy-MM-dd"),
      //     email: this.naccount.email,
      //     gender: this.naccount.gender,
      //   };
      //   if(account.gender == 'nu') account.avt = '/_nuxt/assets/avtgirl.jpg' ;
      //   data.push(account);
      //   data = JSON.stringify(data);
      //   window.localStorage.setItem('account', data);
      //   window.location.reload();
      // }
    },

  editModal: function(id)
  {
    let data = localStorage.getItem('account');
    data = JSON.parse(data);
    let editAccount = data.find((account) => account.id == id);
    this.showDialogEdit = 'nam';
  },

  delModal(id){
    if (confirm('Bạn muốn xóa tài khoản này ?') == true) {
      let data = localStorage.getItem('account');
      data = JSON.parse(data);
      let delAccountIndex = data.findIndex((account) => account.id == id);
      data.splice(delAccountIndex,1);
      data = JSON.stringify(data);
      window.localStorage.setItem('account', data);
      window.location.reload();
    }
  },

  },
}
</script>