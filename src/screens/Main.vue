<template>
  <view class="container">
    <header :style="{width: '100%'}"/>
    <scroll-view class="scroll-view">
    <view :style="{borderTopWidth: 1, borderTopColor: 'gray', width: '100%'}"></view>
      <view class="border" v-for="(team, index) in teams" :key="index"> 
        <view class="flex-container-vertical">
          <text> {{ index+1 }} </text>
          <text :on-press="handlePush">{{ team.name }} </text>
          <text>{{ team.poeng }} </text>
        </view>
      </view>
    <text>{{message}}</text>
    </scroll-view>
  </view>
</template>


<script>
import Header from '../components/Header';

export default {
  name: 'App',
  components: {Header},
  mounted(){
    fetch('https://fantasy.premierleague.com/drf/leagues-classic-standings/1367775?phase=&30.json')
      .then(_bodyInit => _bodyInit.json())
      .then(data => {
        this.teams[0].name = data.standings.results[0].entry_name
        this.teams[0].poeng = data.standings.results[0].total
        this.teams[1].name = data.standings.results[1].entry_name
        this.teams[1].poeng = data.standings.results[1].total
        this.teams[2].name = data.standings.results[2].entry_name
        this.teams[2].poeng = data.standings.results[2].total
      }),
    fetch('https://fantasy.premierleague.com/drf/entry/'+this.teamIds[2].teamId+'/event/30/picks.json')
      // .then(_bodyInit => _bodyInit.json())
      .then(data => {
        this.message = data})
  },
  data(){
    return {
      message: null,
      teams: [
        { name: "", poeng: '5'},
        { name: "", poeng: '3'},
        { name: "", poeng: '6'},
      ],
      teamIds: [
        {name: "Thomas", teamId: "2683986"},
        {name: "Stian", teamId: "1640722"},
        {name: "Vegard", teamId: "2957769"},
      ], 
    }
  },
  props: {
    navigation: {
      type: Object
    }
  },
  created(){
    // console.log(this.test);
    // this.teams[1].name = this.firstPlaceTotal;
  },
  // computed:{
  //   teamName(){
  //     return this.test.filter((event_total) => {return data.event_total.match(this.filterScore); 
  //     })
  //   },
  // },
  methods: {
    handlePush() {
      this.navigation.navigate("Thomas");
    }
    // renderList: (item) => {
    //   return (<Text>{item.teams}</Text>)
    // }
  }
}


</script>

<style>
 .container {
  background-color: rgba(7, 255, 210, 0.05);
  align-items: center;
  justify-content: center;
  flex: 1;
}
.text-color-primary {
  color: blue;
} 
.scroll-view {
    width: 100%;
    /* padding-top: 20px; */
    /* padding-bottom: 30px; */
}
.loading-container {
    height: 600px;
}
.border {
  border-bottom-width: 1;
  border-color: grey;
  width: 100%;
  padding: 15;
}
.flex-container-vertical {
  align-items: center;
  flex-basis: 100px;
}
.flex-container-horisontal {
  flex-direction: row;
  align-items: center;
  flex-basis: 100px;
}
</style>
