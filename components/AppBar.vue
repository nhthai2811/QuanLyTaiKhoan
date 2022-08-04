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
            <NuxtLink to="/createAccount">
              <md-button md-menu-trigger>Tạo tài khoản</md-button>
            </NuxtLink>
          </md-list-item>
        </md-list>
      </md-app-drawer>

      <md-app-content>
        <div>
          <md-button class="md-dense md-raised md-primary" v-on:click="getData('List')" @click="viewmode = 'list'">List</md-button>
          <md-button class="md-dense md-raised md-primary" v-on:click="getData('Card')" @click="viewmode = 'card'">Card</md-button>
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
                <md-button>Action</md-button>
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
              </md-list-item>
            </div>
        </div>
        
      </md-app-content>
    </md-app>
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
</style>

<script>
export default {
  name: 'RegularSwitch',
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
        }
      ],
      switchs: 0,
      radio: 'accent',
      viewmode: 'list',
    }
  },
  methods:{
    getData(data)
    {

    }
  },
}
</script>