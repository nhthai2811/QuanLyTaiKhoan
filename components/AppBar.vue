<template>
  <div class="page-container">
    <md-app>
      <md-app-toolbar >
        <md-field id="search-input">
          <md-input></md-input>
        </md-field>
      </md-app-toolbar>

      <md-app-drawer md-permanent="full">
        <md-list>
          <md-list-item>
            <NuxtLink to="/">
              <md-button md-menu-trigger>Quản lý tài khoản</md-button>
            </NuxtLink>
          </md-list-item>
          <md-list-item>
              <md-button md-menu-trigger @click="showDialog = true">Tạo tài khoản</md-button>
          </md-list-item>
        </md-list>
      </md-app-drawer>

      <md-app-content>
        <div>
          <md-button class="md-dense md-raised md-primary" @click="viewmode = 'list'">List</md-button>
          <md-button class="md-dense md-raised md-primary" @click="viewmode = 'card'">Card</md-button>
        </div>
        <div v-for="account in accounts" :key="account._id" >
            <div v-if="viewmode === 'card'" class="md-card">
              <div class="md-card-header">
                <div class="md-title">Card without hover effect</div>
              </div>
              <div class="md-card-content">
                Lorem ipsum dolor sit amet, consectetur adipisicing elit. Optio itaque ea, nostrum odio. Dolores, sed accusantium quasi non.
              </div>

              <div class="md-card-actions">
                <md-button md-menu-trigger @click="showDialogEdit = true">Sửa</md-button>
                <md-button>Action</md-button>
              </div>
            </div>
            <div v-if="viewmode === 'list'" class="md-list">
              <md-list-item class="info-box">
                <md-avatar>
                  <img src="https://placeimg.com/40/40/people/1" alt="People">
                </md-avatar>
                <div class="md-list-item-text">
                  <span>{{account.name}}</span>
                  <span>{{account.username}}</span>
                  <span>{{account.email}}</span>
                  <p>{{account.address}}</p>
                  <span>{{account.date}}</span>
                </div>
                <md-button md-menu-trigger @click="showDialogEdit = true">Sửa</md-button>
              </md-list-item>
            </div>
        </div>
      </md-app-content>
    </md-app>

    <div>
      <md-dialog :md-active.sync="showDialog">
        <md-dialog-title>Thêm</md-dialog-title>

        <form class="createForm" id="create">
            <md-field class="md-field-dialog">
              <label>Họ và tên</label>
              <md-input v-model="editAccount.name" name="name"></md-input>
            </md-field>

            <md-field class="md-field-dialog">
              <label>Email</label>
              <md-input v-model="editAccount.email" name="email"></md-input>
            </md-field>

            <md-field class="md-field-dialog">
              <label>Mật khẩu</label>
              <md-input v-model="editAccount.pw" type="password" name="pw"></md-input>
            </md-field>

            <md-field class="md-field-dialog">
              <label>Nhập lại mật khẩu</label>
              <md-input v-model="editAccount.cpw" type="password" name="cpw"></md-input>
            </md-field>

            <md-field class="md-field-dialog">
              <label>Số điện thoại</label>
              <md-input v-model="editAccount.date"></md-input>
            </md-field>

            
                <md-field class="md-field-dialog">
                  <label for="movie">Giới tính</label>
                  <md-select name="movie" id="movie" disabled>
                    <md-option value="fight-club">Fight Club</md-option>
                    <md-option value="godfather">Godfather</md-option>
                    <md-option value="godfather-ii">Godfather II</md-option>
                    <md-option value="godfather-iii">Godfather III</md-option>
                    <md-option value="godfellas">Godfellas</md-option>
                    <md-option value="pulp-fiction">Pulp Fiction</md-option>
                    <md-option value="scarface">Scarface</md-option>
                  </md-select>
                </md-field>
                

            <md-field class="md-field-dialog">
              <label>Địa chỉ</label>
              <md-textarea v-model="editAccount.address" name="address"></md-textarea>
            </md-field>

            <md-card-actions>
              <md-button type="submit" class="md-primary"  @click.prevent="onSave">Tạo tài khoản</md-button>
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
              <label>Họ và tên</label>
              <md-input v-model="editAccount.name" name="name"></md-input>
            </md-field>

            <md-field class="md-field-dialog">
              <label>Email</label>
              <md-input v-model="editAccount.email" name="email"></md-input>
            </md-field>

            <md-field class="md-field-dialog">
              <label>Mật khẩu</label>
              <md-input v-model="editAccount.pw" type="password" name="pw"></md-input>
            </md-field>

            <md-field class="md-field-dialog">
              <label>Nhập lại mật khẩu</label>
              <md-input v-model="editAccount.cpw" type="password" name="cpw"></md-input>
            </md-field>

            <md-field class="md-field-dialog">
              <label>Số điện thoại</label>
              <md-input v-model="editAccount.date"></md-input>
            </md-field>

            
                <md-field class="md-field-dialog">
                  <label for="movie">Giới tính</label>
                  <md-select name="movie" id="movie" disabled>
                    <md-option value="fight-club">Fight Club</md-option>
                    <md-option value="godfather">Godfather</md-option>
                    <md-option value="godfather-ii">Godfather II</md-option>
                    <md-option value="godfather-iii">Godfather III</md-option>
                    <md-option value="godfellas">Godfellas</md-option>
                    <md-option value="pulp-fiction">Pulp Fiction</md-option>
                    <md-option value="scarface">Scarface</md-option>
                  </md-select>
                </md-field>
                

            <md-field class="md-field-dialog">
              <label>Địa chỉ</label>
              <md-textarea v-model="editAccount.address" name="address"></md-textarea>
            </md-field>

            <md-card-actions>
              <md-button type="submit" class="md-primary"  @click.prevent="onSave">Tạo tài khoản</md-button>
              <md-button class="md-primary" @click="showDialogEdit = false">Close</md-button>
            </md-card-actions>
          </form>
      </md-dialog>
    </div>
  </div>
</template>

<style lang="css" scoped>

.md-card {
    width: 320px;
    margin: 4px;
    display: inline-block;
    vertical-align: top;
    float: left;
  }
.info-box{
    list-style-position:inside;
    border: 1px solid black;
    margin: 1px;
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
</style>

<script>
// let account = [
// //         accounts: [
//         {
//            _id: 1,
//           name: 'Nguyen Hoang Thai',
//           username: 'nhthai12',
//           email: 'hoangthai123@gmail.com',
//           address: 'so 2538 to 1 ap Thuan Thanh xa Thuan An thi xa Binh Minh tinh Vinh Long',
//           date: '0343579108'
//         },
//         {
//           _id: 2,
//           name: 'Nguyen Hoang Thong',
//           username: 'nhthong1',
//           email: 'hoangthong123@gmail.com',
//           address: 'so 2538 to 1 ap Thuan Thanh xa Thuan An thi xa Binh Minh tinh Vinh Long',
//           date: '0903456471'
//         },
//         {
//           _id: 3,
//           name: 'Nguyen Hoang Phu',
//           username: 'nhphu123',
//           email: 'hoangphu123@gmail.com',
//           address: 'so 1234 to 5 ap Tuan Hoang xa Phu Quan huyen Tra On tinh Vinh Long',
//           date: '0121568423'
//         },
//       ]
// ]
// account = JSON.stringify(account);
// if (process.browser) {
//   window.localStorage.setItem('account', account);
// }

  // if (process.browser) {
  //  let accounts1 =  window.localStorage.getItem('account');
  // //  account1 = JSON.parseJson(accounts1);
  //  console.log(accounts1);
  // }
  
  

export default {
  name: 'RegularSwitch',
  props: {
    account: {
      type: Object,
      default: {
        name: '',
        username: '',
        pw: '',
        cpw: '',
        address: '',
        date: '',
      }
    }
  },

  data() {
      return {
        accounts: [
        {
           _id: 1,
          name: 'Nguyen Hoang Thai',
          username: 'nhthai12',
          email: 'hoangthai123@gmail.com',
          address: 'so 2538 to 1 ap Thuan Thanh xa Thuan An thi xa Binh Minh tinh Vinh Long',
          date: '0343579108'
        },
        {
          _id: 2,
          name: 'Nguyen Hoang Thong',
          username: 'nhthong1',
          email: 'hoangthong123@gmail.com',
          address: 'so 2538 to 1 ap Thuan Thanh xa Thuan An thi xa Binh Minh tinh Vinh Long',
          date: '0903456471'
        },
        {
          _id: 3,
          name: 'Nguyen Hoang Phu',
          username: 'nhphu123',
          email: 'hoangphu123@gmail.com',
          address: 'so 1234 to 5 ap Tuan Hoang xa Phu Quan huyen Tra On tinh Vinh Long',
          date: '0121568423'
        },
      ],   
      
      switchs: 0,
      radio: 'accent',
      viewmode: 'list',
      showDialog: false,
      showDialogEdit: false,
      isSubmit: false,

        editAccount: this.account ? {...this.account } : {
        name: '',
        username: '',
        pw: '',
        cpw: '',
        address: '',
        date: '',
      }
    }
  },

  methods:{
    onSave()
    {
      this.showDialog = false;
      
    }
  },
}
</script>