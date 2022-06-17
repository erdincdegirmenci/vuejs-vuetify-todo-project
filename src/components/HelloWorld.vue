<template>
<div>
  <v-container>
    <v-row class="text-center">
      <v-col cols="12">
        <v-img
          :src="require('../assets/logo.svg')"
          class="my-3"
          contain
          height="200"
        />
      </v-col>

      <v-col class="mb-4">
        <h1 class="display-2 font-weight-bold mb-3">
          TO DO LIST
        </h1>
      </v-col>

      <v-col
        class="mb-5"
        cols="12"
      >
      <v-form
    ref="form"
    v-model="valid"
    lazy-validation
  >
    <v-text-field
      v-model="task"
      :counter="10"
      :rules="todoRules"
      label="Task"
      required
    ></v-text-field>

   
    <v-btn
      :disabled="!valid"
      color="success"
      class="mr-4"
      @click="addTodo"
    >
      Add
    </v-btn>

    <v-btn
      color="error"
      class="mr-4"
      @click="reset"
    >
      CLEAR
    </v-btn>
  </v-form>
      </v-col>


    </v-row>
  </v-container>
    <v-container>
    <v-row class="text-center">
        <v-col
        class="mb-5"
        cols="12"
      >
  <v-simple-table>
      <template v-slot:default>
        <thead>
          <tr>
            <th class="text-left">
              
            </th>
            <th class="text-left">
              
            </th>
          </tr>
        </thead>
        <tbody>
          <tr
            v-for="item in todoData"
            :key="item.Id"
          >
            <td>{{ item.Todo }}</td>
            <td>    <v-btn
              @click="deleteToDo(item.Id)"
      depressed
      color="error"
    >
      Delete
    </v-btn></td>
          </tr>
        </tbody>
      </template>
    </v-simple-table>
        </v-col>
    </v-row>
    </v-container>
</div>
</template>

<script>
  export default {
    task: 'HelloWorld',

    data: () => ({
      todoData: [],
      valid: true,
      task: '',
      todoRules: [
        v => !!v || 'Field is required'
      ],
      ecosystem: [
        {
          text: 'vuetify-loader',
          href: 'https://github.com/vuetifyjs/vuetify-loader',
        },
        {
          text: 'github',
          href: 'https://github.com/vuetifyjs/vuetify',
        },
        {
          text: 'awesome-vuetify',
          href: 'https://github.com/vuetifyjs/awesome-vuetify',
        },
      ],
      importantLinks: [
        {
          text: 'Documentation',
          href: 'https://vuetifyjs.com',
        },
        {
          text: 'Chat',
          href: 'https://community.vuetifyjs.com',
        },
        {
          text: 'Made with Vuetify',
          href: 'https://madewithvuejs.com/vuetify',
        },
        {
          text: 'Twitter',
          href: 'https://twitter.com/vuetifyjs',
        },
        {
          text: 'Articles',
          href: 'https://medium.com/vuetify',
        },
      ],
      whatsNext: [
        {
          text: 'Explore components',
          href: 'https://vuetifyjs.com/components/api-explorer',
        },
        {
          text: 'Select a layout',
          href: 'https://vuetifyjs.com/getting-started/pre-made-layouts',
        },
        {
          text: 'Frequently Asked Questions',
          href: 'https://vuetifyjs.com/getting-started/frequently-asked-questions',
        },
      ],
    }),
    methods: {
      reset () {
        this.$refs.form.reset()
      },
      addTodo (){
        if(this.$refs.form.validate())
        {
          this.todoData.push({ Id: Math.ceil(Math.random()*10), Todo: this.task})
        }
      },
      deleteToDo(todoId){
          var index = this.todoData.findIndex(x => x.Id === todoId)
          this.todoData.splice(index, 1)
      }
    }
  }    
</script>
