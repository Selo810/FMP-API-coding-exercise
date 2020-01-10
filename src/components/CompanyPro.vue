<template>
  <v-card
    class="mx-auto mt-12"
    max-width="800"
  >
    <v-card-title>{{title}}</v-card-title>
    <v-system-bar></v-system-bar>

    <v-toolbar
      flat
      color="transparent"
    >
      <v-text-field
        v-model="search"
        label="Search by Symbol ex: AAPL"
        single-line
      ></v-text-field>
      <v-btn icon @click="getData(search)">
        <v-icon>mdi-magnify</v-icon>
      </v-btn>
    </v-toolbar>

    <v-list three-line>
      <v-list-item
        v-for="(item, i) in company"
        :key="i"
        ripple
      >
        <v-img
          :src="item.image"
          class="mr-4"
          max-width="64"
          min-width="64"
        ></v-img>
        
        <v-list-item-content>
        <h3>{{item.companyName}}</h3>

        <div v-text="item.description"></div>
          <v-divider></v-divider>
          
        <div>
            <v-row>
              <v-col cols="12" sm="6" v-if="item.changes">
                  <b>Stock Price Change: </b> 
                  <span v-if='item.changes > 0' style="color: green">{{item.changes}}</span>
                  <span v-else style="color: red">{{item.changes}}</span>
              </v-col>
                
              <v-col cols="12" sm="6" v-if="item.changesPercentage">  
                  <b>Change Percentage: </b> 
                  <span style="color: green" v-if="item.changesPercentage.includes('+')">{{item.changesPercentage}}</span>
                  <span style="color: red" v-if="item.changesPercentage.includes('-')">{{item.changesPercentage}}</span>
              </v-col>
            </v-row>

            <v-row>
              <v-col cols="12" sm="6" v-if="item.price">
                <p> <b>Price: </b> &#36;{{item.price}}</p>
              </v-col>
              <v-col cols="12" sm="6">
                <p> <b>52 week range: </b> {{item.range}}</p>
              </v-col>
            </v-row>

            <v-row>
              <v-col cols="12" sm="6">
                <p> <b>Beta: </b>{{item.beta}}</p>
              </v-col>
              <v-col cols="12" sm="6">
                <p> <b>Volume Average: </b> {{item.volAvg}}</p>
              </v-col>
            </v-row>

            <v-row>
              <v-col cols="12" sm="6">
                <p> <b>Market Capitalisation: </b>{{item.mktCap}}</p>
              </v-col>
              <v-col cols="12" sm="6">
                <p> <b>Last Dividend: </b> {{item.lastDiv}}</p>
              </v-col>
            </v-row>

            <v-row>
              <v-col cols="12" sm="6">
                <p> <b>Exchange: </b> {{item.exchange}}</p>
              </v-col>
              <v-col cols="12" sm="6">
                <p> <b>Industry: </b> {{item.industry}}</p>
              </v-col>
            </v-row>

             <v-row>
              <v-col cols="12" sm="6">
                <p> <b>CEO: </b> {{item.ceo}}</p>
              </v-col>
              <v-col cols="12" sm="6">
                <p> <b>Sector: </b> {{item.sector}}</p>
              </v-col>
            </v-row>
        </div>
        </v-list-item-content>
        <v-card-actions>
          <v-btn class="ma-2" color="orange darken-2" dark @click="explore(item.website)">
            Explore<v-icon dark right>mdi-arrow-right</v-icon>
          </v-btn>
        </v-card-actions>
        
      </v-list-item>
      <v-divider></v-divider>
      <v-divider></v-divider>
    </v-list>
    
  </v-card>
</template>

<script>
import axios from "axios";
export default {
  components: {
  },

  data: () => ({
    search: '',
    url: 'https://financialmodelingprep.com/api/v3/company/profile/AAPL',
    company: [],
    loaded: false,
    title: 'Company Search Page'
  }),

  computed: {

  },

  mounted() {
      //this.getData();
  },

  methods: {
    getData: async function(symbol) {
        var vm = this

        if (!this.search) return this.company;

        axios.get('https://financialmodelingprep.com/api/v3/company/profile/'+symbol)
        .then((response) => {
          if(response.data.profile){
            let company = [response.data.profile]; 
            vm.company = company;
          }else{
            alert('Sorry, we couldnot find any company with that symbol!!');
            vm.company = [];
          }
            
        })
        .catch((error) => {
            alert(error);
        })
    },

    //Open external link
    explore(url){
        window.open(url, '_blank');
    }
    
  }
};
</script>
