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
        <form>
          <md-field>
            <label>Họ và tên</label>
            <md-input v-model="initial"></md-input>
          </md-field>

          <md-field>
            <label>Email</label>
            <md-input v-model="initial"></md-input>
          </md-field>

          <md-field>
            <label>Mật khẩu</label>
            <md-input v-model="password" type="password"></md-input>
          </md-field>

          <md-field>
            <label>Nhập lại mật khẩu</label>
            <md-input v-model="password" type="password"></md-input>
          </md-field>

          <md-field>
            <label>Số điện thoại</label>
            <md-input v-model="number"></md-input>
          </md-field>

          
              <md-field>
                <label for="movie">Giới tính</label>
                <md-select v-model="movie" name="movie" id="movie" disabled>
                  <md-option value="fight-club">Fight Club</md-option>
                  <md-option value="godfather">Godfather</md-option>
                  <md-option value="godfather-ii">Godfather II</md-option>
                  <md-option value="godfather-iii">Godfather III</md-option>
                  <md-option value="godfellas">Godfellas</md-option>
                  <md-option value="pulp-fiction">Pulp Fiction</md-option>
                  <md-option value="scarface">Scarface</md-option>
                </md-select>
              </md-field>
              

          <md-field>
            <label>Địa chỉ</label>
            <md-textarea v-model="textarea"></md-textarea>
          </md-field>

          <md-card-actions>
            <md-button type="submit" class="md-primary" :disabled="sending">Tạo tài khoản</md-button>
          </md-card-actions>
        </form>
      </md-app-content>
    </md-app>
  </div>
</template>

<style lang="css" scoped>

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
    max-height: 100%;
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
</style>

<script>
  export default {
    name: 'DisabledSelect',
    data: () => ({
      movie: null,
      country: null,
      food: null
    })
  }
</script>