<template>
  <v-content>
      <v-container class="fill-height mt-5" fluid>

      <v-overlay
        v-if="!loaded"
      >
      <div class="text-center">
          <v-progress-circular
            :size="50"
            color="primary"
            indeterminate
          ></v-progress-circular>
        </div></v-overlay>

       <v-row align="center" justify="center">
          <v-col cols="12" sm="8" md="5">
            <v-card>
              <v-card-text>
                <v-form v-model="valid">
                  <v-row align="center" justify="center">
                  </v-row>
                  <v-text-field
                    v-model="login.name"
                    placeholder="Enter Full Name"
                    outlined
                    class="mt-5"
                    label="full Name"
                    name="name"
                    type="text"
                    :rules="passwordRules"
                  />

                  <v-text-field
                    v-model="login.email"
                    placeholder="someone@example.com"
                    outlined
                    :rules="emailRules"
                    class="mt-5"
                    label="Email ID"
                    name="email"
                    type="email"
                    @keyup.enter="loginauth"
                  />

                  <v-text-field
                    id="password"
                    v-model="login.password"
                    outlined
                    placeholder="super secret password"
                    :rules="passwordRules"
                    label="Password"
                    name="password"
                    type="password"
                    @keyup.enter="loginauth"
                  />

                  <v-select
                    v-model="selectO"
                    :items="items"
                    label="Select An Occupation"
                    data-vv-name="select"
                    required
                    :rules="passwordRules"
                    class='occ'
                  ></v-select>

                  <v-select
                    v-model="selectS"
                    :items="statenames"
                    label="Select A State"
                    data-vv-name="select"
                    required
                    :rules="passwordRules"
                  ></v-select>
                </v-form>
              </v-card-text>
              <v-card-actions>
                <v-spacer />
                <v-btn class="white--text" color="#4a7515" :disabled="!valid" large @click="submitForm"
                  >SUBMIT</v-btn
                >
              </v-card-actions>
            </v-card>
          </v-col>
        </v-row>

        <div class="text-center">
    <v-dialog
      v-model="dialog"
      width="500"
      persistent
    >

      <v-card>
        <v-card-title class="text-h5">
          Your form was successfully submitted
        </v-card-title>

        <v-divider></v-divider>

        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            color="#4a7515"
            text
            @click="nav"
          >
            OKAY
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>

      </v-container>
  </v-content>
</template>

<script>


export default {

  components: {
  
  },

  data() {
      return {
        login: {
          email: '',
          password: '',
          name: '',
        },
        valid: true,
        items: [],
        items2: [],
        statenames: [],
        selectO: '',
        selectS:'',

      passwordRules: [
        (v) => !!v || 'Password field is required'
      ],
      emailRules: [
        (v) => !!v || 'Email is required',
        (v) => /.+@.+\..+/.test(v) || 'Email must be valid',
      ],

      snackbar: false,
        text: '',
        color: null,
        loaded: true,
        dialog: false

      }
  },

  mounted() {
      this.occstate()
    },
    methods: {

      loginauth() {
        if(this.login.email == null){
          this.valid = false
        }else{
        }
      },

      async occstate() {
          try{
                const dropdown = await this.$axios.$get(
                'https://frontend-take-home.fetchrewards.com/form')
                this.items = dropdown.occupations;
                this.items2 = dropdown.states;
                for(let i=0;i<this.items2.length;i++){
                    this.statenames.push(this.items2[i].name)
                }
          }catch(error) {
              this.snackbar = true;
              this.color = 'red';
              this.text = 'Oops there was an error loading the form, Try again later';
          }
      },

      async submitForm(){
          this.loaded = false;
          try{
              const dropdown = await this.$axios.$post(
              'https://frontend-take-home.fetchrewards.com/form', 
              {
                name: this.login.name,
                email: this.login.email,
                password: this.login.password,
                occupation: this.selectO,
                state: this.selectS
              })
              this.snackbar = true;
              this.color = 'green';
              this.text = 'Form was successfully submitted';

            //   setTimeout(() => location.reload(), 300);
              this.loaded = true;
              this.dialog = true;
          }catch{
              this.snackbar = true;
              this.color = 'red';
              this.text = 'Oops there was an error, Try again later';
          }
      },

      nav(){
          this.$router.push({ path: '/' })
      }

     
    }
}
</script>

<style>
.btncolor {
  color: #F76F72 !important;
}
.occ {
    cursor: pointer;
}
</style>