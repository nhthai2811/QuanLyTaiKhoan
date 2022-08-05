<template>
  
      <div>
      <md-dialog :md-active.sync="showDialog">
        <md-dialog-title>Preferences</md-dialog-title>

        <form class="createForm">
            <md-field class="md-field-dialog">
              <label>Họ và tên</label>
              <md-input v-model="initial"></md-input>
            </md-field>

            <md-field class="md-field-dialog">
              <label>Email</label>
              <md-input v-model="initial"></md-input>
            </md-field>

            <md-field class="md-field-dialog">
              <label>Mật khẩu</label>
              <md-input v-model="password" type="password"></md-input>
            </md-field>

            <md-field class="md-field-dialog">
              <label>Nhập lại mật khẩu</label>
              <md-input v-model="password" type="password"></md-input>
            </md-field>

            <md-field class="md-field-dialog">
              <label>Số điện thoại</label>
              <md-input v-model="number"></md-input>
            </md-field>

            
                <md-field class="md-field-dialog">
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
                

            <md-field class="md-field-dialog">
              <label>Địa chỉ</label>
              <md-textarea v-model="textarea"></md-textarea>
            </md-field>

            <md-card-actions>
              <md-button type="submit" class="md-primary" :disabled="sending">Tạo tài khoản</md-button>
              <md-button class="md-primary" @click="showDialog = false">Close</md-button>
            </md-card-actions>
          </form>
      </md-dialog>

      <md-button class="md-primary md-raised" @click="showDialog = true">Show Dialog</md-button>
    </div>

</template>

<style lang="css" scoped>


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
  export default {
    name: 'DisabledSelect',
    data: () => ({
      movie: null,
      country: null,
      food: null,
      showDialog: true,
    })
  }
</script>