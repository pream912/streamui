<template>
  <v-container>
    <v-row>
      <v-col>
        <v-btn @click="dialog = true" color="green"> Create server </v-btn>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="12">
        <v-data-table
        :headers="mandayan"
        :items="items">
        </v-data-table>
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <v-dialog v-model="dialog" persistent max-width="600px">
          <v-card>
            <v-card-title>
              <span class="headline">User Profile</span>
            </v-card-title>
            <v-card-text>
              <v-container>
                <v-row>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field v-model="sname" label="Server name" required></v-text-field>
                  </v-col>
                </v-row>
              </v-container>
            </v-card-text>
            <v-card-actions>
              <v-btn :loading="loading" :disabled="loading" @click="createServer" color="green">Ok</v-btn>
              <v-btn @click="dialog = false" color="red">Close</v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import axios from 'axios'
  export default {
    name: 'HelloWorld',

    data: () => ({
      dialog: false,
      sname: '',
      mandayan: [
        {text: 'Name', value: 'name'},
        {text: 'IP', value: 'ip'},
        //{text: 'Created', value: 'created'},
        {text: 'Action', value: 'action'}
      ],
      loading: false,
      items: []
    }),

    methods: {
      async createServer () {
        this.loading = true
        console.log('clicked')
        await axios.post('http://34.93.215.34:8080/create', {uid: this.sname})
        .then((res) => {
          console.log(res)
          let data = res.data[0]
          let server = {
            name: data.name,
            ip: data.networkInterfaces[0].accessConfigs[0].natIP
          }
          this.items.push(server)
          this.loading = false
          this.dialog =  false
        })
      }
    }
  }
</script>