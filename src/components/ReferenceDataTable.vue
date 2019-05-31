<template>
  <v-flex xs12>
    <h1>Data Table</h1>
    <div>
      <v-dialog v-model="dialog">
        <v-btn color="primary" slot="activator" class="mb-4 mt-4">New Item</v-btn>
        <v-card>
          <v-card-title>
            <span class="headline">{{ formTitle }}</span>
          </v-card-title>
          <v-card-text>
            <v-container grid-list-md>
              <v-layout wrap>
                <v-flex xs12>
                  <v-text-field
                    label="English"
                    outline
                    v-model="editedItem.english"
                    @keyup="wordsCounter"
                  ></v-text-field>
                  <p>current word counter: {{currentWordsCount}}</p>
                </v-flex>
                <v-flex xs12>
                  <v-text-field label="translation" outline v-model="editedItem.translation"></v-text-field>
                </v-flex>
                <v-flex xs12>
                  {{ selectedPlan }}
                  <v-select
                    v-model="selectedPlan"
                    item-text="label"
                    item-value="value"
                    :items="plans"
                    label="旅行プラン"
                    multiple
                  />
                </v-flex>
              </v-layout>
            </v-container>
          </v-card-text>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn color="gray" @click.native="close">Cancel</v-btn>
            <v-btn color="success" @click.native="save">Save</v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
      <v-data-table :headers="headers" :items="items" hide-actions class="elevation-1">
        <template slot="items" slot-scope="props">
          <td>{{ props.item.english }}</td>
          <td>{{ props.item.translation }}</td>
          <td class="layout px-0">
            <v-btn icon class="mx-0" @click="editItem(props.item)">
              <v-icon color="blue">edit</v-icon>
            </v-btn>
            <v-btn icon class="mx-0" @click="deleteItem(props.item)">
              <v-icon color="pink">delete</v-icon>
            </v-btn>
          </td>
        </template>
        <template slot="no-data">
          <v-btn color="primary" @click="initialize">Reset</v-btn>
        </template>
      </v-data-table>
    </div>
  </v-flex>
</template>

    <script>
/*
https://vuetifyjs.com/ja/components/selects#examples
    */
export default {
  data: () => ({
    dialog: false,
    headers: [
      { text: "English", value: "english" },
      { text: "Translation", value: "translation" },
      { text: "Actions", value: "name", sortable: false }
    ],
    items: [],
    editedIndex: -1,
    editedItem: {
      english: "",
      translation: ""
    },
    defaultItem: {
      english: "",
      translation: ""
    },
    currentWordsCount: 0,
    selectedPlan: { label: "ドイツ", value: "germany" },
    plans: [
      { label: "ドイツ", value: "germany" },
      { label: "スペイン", value: "spain" },
      { label: "フランス", value: "france" }
    ]
  }),

  computed: {
    formTitle() {
      return this.editedIndex === -1 ? "New Item" : "Edit Item";
    }
  },

  watch: {
    dialog(val) {
      val || this.close();
    }
  },

  created() {
    this.initialize();
  },

  methods: {
    initialize() {
      this.items = [
        {
          english: "aaaa bbbb",
          translation: "テスト1"
        },
        {
          english: "aaaa bbbb",
          translation: "テスト2"
        }
      ];
    },

    editItem(item) {
      this.editedIndex = this.items.indexOf(item);
      this.editedItem = Object.assign({}, item);
      this.dialog = true;
    },

    deleteItem(item) {
      const index = this.items.indexOf(item);
      confirm("Are you sure you want to delete this item?") &&
        this.items.splice(index, 1);
    },

    close() {
      this.dialog = false;
      setTimeout(() => {
        this.editedItem = Object.assign({}, this.defaultItem);
        this.editedIndex = -1;
      }, 300);
    },

    save() {
      if (this.editedIndex > -1) {
        Object.assign(this.items[this.editedIndex], this.editedItem);
      } else {
        this.items.push(this.editedItem);
      }
      this.close();
    },

    wordsCounter() {
      var wordsNum = this.english.split(" ").length;
      this.currentWordsCount = wordsNum;
    }
  }
};
</script>
