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
            <md-button md-menu-trigger v-on:click="openCreateModal" class="btmenu">Tạo tài khoản</md-button>
          </md-list-item>
        </md-list>
      </md-app-drawer>

      <md-app-content>
        <div v-if="viewmode === 'list'">
          <md-button class="md-dense md-raised md-mini md-fab-bottom-right md-primary" @click="viewmode = 'list'">List
          </md-button>
          <md-button class="md-dense md-raised md-mini md-fab-bottom-right" @click="viewmode = 'card'">Card</md-button>
        </div>
        <div v-if="viewmode === 'card'">
          <md-button class="md-dense md-raised md-mini" @click="viewmode = 'list'">List</md-button>
          <md-button class="md-dense md-raised md-mini md-primary" @click="viewmode = 'card'">Card</md-button>
        </div>
        <div id="listAccount">
          <div v-for="account in accounts" :key="account._id" :class="'md-elevation-2 info-box md-' + viewmode">
            <div v-if="viewmode === 'card'" class="md-with-hover">
              <md-card-header>
                <md-card-header-text>
                  <span><b><span>Tên:</span></b> {{ account.name }}</span><br>
                  <span><b><span>Tên tài khoản:</span></b>{{ account.username }}</span><br>
                  <span><b><span>Ngày sinh: </span></b>{{ account.date }}</span><br>
                  <span v-if="account.gender=='nam'"><b><span>Giới tính: </span></b>Nam</span>
                  <span v-if="account.gender=='nu'"><b><span>Giới tính: </span></b>Nữ</span>
                  <br><span><b><span>Email: </span></b>{{ account.email }}</span><br>
                  <span><b><span>Địa chỉ: </span></b>{{ account.address }}</span>
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
            <div v-if="viewmode === 'list'" class="md-list-hover" id="listAcc">
              <md-list-item>
                <md-avatar>
                  <img class="avt" :src="account.avt" alt="People">
                </md-avatar>
                <div class="md-list-item-text">
                  <span><b><span>Tên:</span></b> {{ account.name }}</span>
                  <span><b><span>Tên tài khoản:</span></b>{{ account.username }}</span>
                  <span><b><span>Ngày sinh: </span></b>{{ account.date }}</span>
                  <span v-if="account.gender=='nam'"><b><span>Giới tính: </span></b>Nam</span>
                  <span v-if="account.gender=='nu'"><b><span>Giới tính: </span></b>Nữ</span>
                  <span><b><span>Email: </span></b>{{ account.email }}</span>
                  <span><b><span>Địa chỉ: </span></b>{{ account.address }}</span>
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

      <div class="modal" id="openAccountModal" style="z-index: 10">
        <div class="modal-dialog modal-lg modal-dialog-centered">
          <div class="modal-content">

            <!-- Modal Header -->
            <div class="modal-header">
              <h4 class="modal-title">Thêm tài khoản</h4>
              <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
            </div>

            <!-- Modal body -->
            <div class="modal-body">

              <form class="createForm" id="create" name="createForm" v-on:submit.prevent="onSubmit()">
                <md-field class="md-field-dialog" :md-counter="false">
                  <label>Tên tài khoản</label>
                  <md-input v-model="naccount.username" name="username" maxlength="8"></md-input>
                </md-field>
                <div class="error" v-if="errors.username">{{ errors.username }}</div>
                <md-field class="md-field-dialog" :md-counter="false">
                  <label>Họ và tên</label>
                  <md-input v-model="naccount.name" name="name" maxlength="20"></md-input>
                </md-field>
                <md-field class="md-field-dialog">
                  <label>Email</label>
                  <md-input v-model="naccount.email" name="email" ></md-input>
                </md-field>
                <div class="error" v-if="errors.email">{{ errors.email }}</div>
                <div class="md-field-dialog">
                  <md-datepicker v-model="naccount.date">
                    <label>Ngày sinh</label>
                    <span class="md-helper-text">yyyy-mm-dd</span>
                  </md-datepicker>
                </div>
                <div class="error" v-if="errors.date">{{ errors.date }}</div>
                <div class="md-field-dialog">
                  <div>
                    <div class="form-check form-check-inline">
                      <input class="form-check-input" type="radio" name="gender" id="genderNam" value="nam"
                             v-model="naccount.gender">
                      <label class="form-check-label" for="inlineRadio1">Nam</label>
                    </div>
                    <div class="form-check form-check-inline">
                      <input class="form-check-input" type="radio" name="gender" id="genderNu" value="nu"
                             v-model="naccount.gender">
                      <label class="form-check-label" for="inlineRadio2">Nữ</label>
                    </div>
                  </div>
                </div>
                <div class="error" v-if="errors.gender">{{ errors.gender }}</div>
                <md-field class="md-field-dialog" :md-counter="false">
                  <label>Địa chỉ</label>
                  <md-textarea v-model="naccount.address" maxlength="200" md-autogrow></md-textarea>
                </md-field>
                <div class="error" v-if="errors.address">{{ errors.address }}</div>
                <md-card-actions class="btmodal">
                  <md-button type="submit" class="md-primary">Tạo tài khoản</md-button>
                  <md-button class="md-primary" v-on:click="backcreateModal">Close</md-button>
                </md-card-actions>
              </form>

            </div>
          </div>
        </div>
      </div>

    </div>

    <!-- The Modal -->
    <div class="modal" id="editAccount" style="z-index: 10">
      <div class="modal-dialog modal-lg modal-dialog-centered">
        <div class="modal-content">

          <!-- Modal Header -->
          <div class="modal-header">
            <h4 class="modal-title">Sửa thông tin</h4>
            <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
          </div>

          <!-- Modal body -->
          <div class="modal-body">

            <form class="createForm" id="editForm" name="createForm">
              <input type="hidden" id="idAccount">
              <md-field class="md-field-dialog" :md-counter="false">
                <label>Tên tài khoản</label>
                <md-input name="username" maxlength="8" id="editUsername"></md-input>
                <!--                <md-input name="username" maxlength="8" id="editUsername"></md-input>-->
              </md-field>

              <div class="error err-username"></div>
              <md-field class="md-field-dialog" :md-counter="false">
                <label>Họ và tên</label>
                <md-input name="name" maxlength="20" id="editName"></md-input>
                <!--                <md-input name="name" maxlength="20" id="editName"></md-input>-->
              </md-field>
              <div class="error err-name"></div>
              <md-field class="md-field-dialog">
                <label>Email</label>
                <md-input name="email" id="editEmail"></md-input>
              </md-field>
              <div class="error err-email"></div>
              <div class="md-field-dialog date">
                <md-datepicker>
                  <label>Ngày sinh</label>
                  <span class="md-helper-text">yyyy-mm-dd</span>
                </md-datepicker>
              </div>
              <div class="error err-date"></div>
              <div class="md-field-dialog">
                <div class="form-check form-check-inline">
                  <input class="form-check-input" type="radio" name="gender" id="editgenderNam" value="nam">
                  <label class="form-check-label" for="inlineRadio1">Nam</label>
                </div>
                <div class="form-check form-check-inline">
                  <input class="form-check-input" type="radio" name="gender" id="editgenderNu" value="nu">
                  <label class="form-check-label" for="inlineRadio2">Nữ</label>
                </div>
              </div>
              <md-field class="md-field-dialog" :md-counter="false">
                <label>Địa chỉ</label>
                <md-textarea maxlength="200" md-autogrow id="editAddress"></md-textarea>
              </md-field>
              <div class="error err-address"></div>
              <md-card-actions class="btmodal">
                <md-button class="md-primary" onclick="window.onSave()">Lưu lại</md-button>
                <md-button class="md-primary" @click.prevent="back">Hủy</md-button>
              </md-card-actions>
            </form>
          </div>
        </div>
      </div>
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

.md-app-drawer, .menu {
  background-color: #448aff;
}

.menu {
  margin-top: 30px;
}

.btmodal {
  margin-bottom: 30px;
}

.btmenu {
  color: #fff;
  margin: 10px;
}

.md-card {
  width: 400px;
  margin: 4px;
  display: inline-block;
  vertical-align: top;
  float: left;
}

.info-box {
  list-style-position: inside;
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

.md-dialog-container .md-theme-default {
  width: 450px;
}

.error {
  color: red;
  font-size: 75%;
  margin-left: 10%;
}

.modal-dialog {
  z-index: 10 !important;
}

.md-card-header-text {
  height: 170px;
  overflow-y: auto;
  overflow-x: hidden;
}

#editAccount .md-field label {
  pointer-events: auto;
  top: 0;
  opacity: 1;
  font-size: 12px;
}

</style>

<script>
import format from 'date-fns/format';
import {parse, isValid} from 'date-fns';
import {enGB} from 'date-fns/locale';
import isMatch from 'date-fns/isMatch'
import Vue from 'vue'
import VueMaterial from 'vue-material'
import 'vue-material/dist/vue-material.min.css'
import 'vue-material/dist/theme/default.css'


Vue.use(VueMaterial);


export default {
  name: 'RegularSwitch',
  data() {
    return {
      accounts: [],
      naccount: [],
      editAccount: [],
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

    }
  },

  created() {
    if (process.browser) {
      let data = localStorage.getItem('account');
      data = JSON.parse(data);
      this.accounts = data;
      $("#listAccount").sortable();

      window.onSave = function () {
        let editAccount =
          {
            id: $('#idAccount').val(),
            username: $('#editUsername').val(),
            name: $('#editName').val(),
            email: $('#editEmail').val(),
            address: $('#editAddress').val(),
            gender: $('input[name=gender]:checked').val(),
            date: $('#editAccount .md-datepicker input').val(),
            avt: 'avtboy.jpg',
          };

        if (editvalidate()) {
          if (editAccount.gender == 'nu') editAccount.avt = 'avtgirl.jpg';
          let data = localStorage.getItem('account');
          data = JSON.parse(data);
          let delAccountIndex = data.findIndex((account) => account.id == editAccount.id);
          data.splice(delAccountIndex, 1);
          data.push(editAccount);
          data = JSON.stringify(data);
          window.localStorage.setItem('account', data);
          window.location.reload();
        }
      };

      function editvalidate() {
        let editAccount =
          {
            username: $('#editUsername').val(),
            name: $('#editName').val(),
            email: $('#editEmail').val(),
            address: $('#editAddress').val(),
            gender: $('input[name=gender]:checked').val(),
            date: $('#editAccount .md-datepicker input').val(),
          }
        let isValid = true;
        if (!editAccount.username) {
          isValid = false;
          $('.err-username').text('Bạn cần nhập tên tài khoản.');
        } else {
          const nameRegex = /^[a-zA-Z0-9]+$/;
          let checkusername = editAccount.username.match(nameRegex);
          if (checkusername == null) {
            $('.err-username').text('Tên tài khoản không đúng quy định');
            isValid = false;
          }
        }
        if (!editAccount.date) {
          $('.err-date').text('Bạn cần chọn ngày sinh.');
          isValid = false;
        }
        if (isMatch(editAccount.date, 'yyyy-mm-dd') == false) {
          $('.err-date').text('Ngày không hợp lệ.');
          isValid = false;
        }
        if (!editAccount.address) {
          $('.err-address').text('Bạn cần nhập địa chỉ.');
          isValid = false;
        }
        if (!editAccount.gender) {
          $('.err-address').text('Bạn cần chọn giới tính');
          isValid = false;
        }
        if (!editAccount.email) {
          $('.err-email').text('Bạn cần nhập email.');
          isValid = false;
        } else {
          const nameRegex = /^(([^<>()[\]\.,;:\s@\"]+(\.[^<>()[\]\.,;:\s@\"]+)*)|(\".+\"))@(([^<>()[\]\.,;:\s@\"]+\.)+[^<>()[\]\.,;:\s@\"]{2,})$/i;
          let checkemail = editAccount.email.match(nameRegex);
          if (checkemail == null) {
            $('.err-email').text('Email không hợp lệ');
            isValid = false;
          }
        }
        return isValid;
      };

      $('#editAccount').on('show.bs.modal', function (e) {
        $(this).find('.error').text('');
      })

    }
  },


  methods: {

    validate() {
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
      } else {
        const nameRegex = /^[a-zA-Z0-9]+$/;
        let checkusername = this.naccount.username.match(nameRegex);
        if (checkusername == null) {
          this.errors.username = "Tên tài khoản không đúng quy định.";
          isValid = false;
        }
      }
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
      } else {
        const nameRegex = /^(([^<>()[\]\.,;:\s@\"]+(\.[^<>()[\]\.,;:\s@\"]+)*)|(\".+\"))@(([^<>()[\]\.,;:\s@\"]+\.)+[^<>()[\]\.,;:\s@\"]{2,})$/i;
        let checkemail = this.naccount.email.match(nameRegex);
        if (checkemail == null) {
          this.errors.email = "Email không hợp lệ.";
          isValid = false;
        }
      }
      return isValid;
    },


    onSubmit() {
      if (this.validate()) {
        this.showDialog = false;
        if (process.browser) {
          let data = localStorage.getItem('account');
          data = JSON.parse(data);
          if (!data) {
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
              address: this.naccount.address,
            };
          if (account.gender == 'nu') account.avt = 'avtgirl.jpg';
          data.push(account);
          data = JSON.stringify(data);
          window.localStorage.setItem('account', data);
          window.location.reload();
        }
      }
    },

    editModal: function (id) {
      if (process.browser) {
        let data = localStorage.getItem('account');
        data = JSON.parse(data);
        let editAccount = data.find((account) => account.id == id);

        $('#editAccount').modal('toggle');
        $('#editUsername').val(editAccount.username);
        $('#editName').val(editAccount.name);
        $('#editEmail').val(editAccount.email);
        $('#editAddress').val(editAccount.address);
        $('#idAccount').val(editAccount.id);
        $('#nameAccount').val(editAccount.name);
        $('#usernameAccount').val(editAccount.username);
        if (editAccount.gender == 'nam') {
          $('#editgenderNam').prop('checked', true);
        } else {
          $('#editgenderNu').prop('checked', true);
        }
        $('#editAccount .md-datepicker input').val(editAccount.date);
      }
    },

    back() {
      $('#editAccount').modal('hide');
    },

    backcreateModal() {
      $('#openAccountModal').modal('hide');
    },

    openCreateModal() {
      $('#openAccountModal').modal('show');
    },

    delModal(id) {
      if (confirm('Bạn muốn xóa tài khoản này ?') == true) {
        let data = localStorage.getItem('account');
        data = JSON.parse(data);
        let delAccountIndex = data.findIndex((account) => account.id == id);
        data.splice(delAccountIndex, 1);
        data = JSON.stringify(data);
        window.localStorage.setItem('account', data);
        window.location.reload();
      }
    },

  },
}
</script>
