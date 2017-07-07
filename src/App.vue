<template>
  <div id="app">
    <!--<img src="./assets/logo.png">-->
    <!--<router-view></router-view>-->

    <div id="player" class="container">
      <ul class="player_box row">
      <li v-for="player in players">
        <span v-bind:key="player.id" class="default_item btn col-2" v-bind:class="{active_item: activePlayer == player.id}" v-on:click="select_player(player.id)">{{ player.name }}</span>
        <span v-for="card in player.own" class="default_item" v-bind:class="{active_item: card.hasSelected}" v-on:click="unselect_card(card.id)">{{ card.type }},{{ card.point }}</span>
      </li>
      </ul>
    </div>
    <div id="pubcard">
      <ul class="player_box">
      </ul>
    </div>
    <div id="poker">
      <ul class="card_box" v-for="p in poker_style">
        <li class="li" v-for="card in p"  v-bind:class="{active_item: card.hasSelected}" v-on:click="select_card(card.id)">{{ card.type }},{{ card.point }}</li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    const _players = []
    const _pokerStyle = []
    const _cards = []
    for (let i = 0; i < 6; i++) {
      _players[i] = {
        name: 'P' + i,
        id: i,
        own: []
      }
    }
    for (let j = 0; j < 4; j++) {
      let _p = []
      for (let i = 0; i < 13; i++) {
        _p[i] = {
          id: 13 * j + i,
          type: j,
          point: i,
          hasSelected: false
        }
        _cards.push(_p[i])
      }
      _pokerStyle[j] = _p
    }
    return {
      msg: 'Welcome to Your Vue.js App',
      players: _players,
      poker_style: _pokerStyle,
      cards: _cards,
      activePlayer: 0
    }
  },
  methods: {
    select_player: function (id) {
      this.activePlayer = id
    },
    select_card: function (id) {
      if (this.players[this.activePlayer].own.length === 4) {
        alert('a position own 4 card max!')
        return
      }
      if (!this.cards[id].hasSelected) {
        this.players[this.activePlayer].own.push(this.cards[id])
        this.cards[id].hasSelected = true
      }
    },
    unselect_card: function (id) {
      for (let card in this.players[this.activePlayer].own) {
        if (card.id === id) this.players.own.splice(this.card[id])
      }
    }
  }
}
</script>

<style>
  body{
    padding: 0 0 0 0;
  }
  ul:after {
    content: '';
    display: block;
    clear: both;
    height: 0;
    visibility: hidden;
  }
  #app {
    clear: both;
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 0px;
  }
  #player{
    clear: both;
    height:auto;
    min-height:200px;
    background-color: azure;
    width: 100%;
  }

  #pubcard{
    clear: both;
    height:auto;
    min-height:200px;
    background-color: #fad0cd;
    width: 100%;
  }
  #poker{
    clear: both;
    height:auto;
    min-height:400px;
    background-color: cornsilk;
    width: 100%;
  }
  .player_box{
    list-style: none;
  }
  .player_box li{
    float: left;
    width: 18%;
  }
  .active_item{
    border-color: salmon;
    color: salmon;
  }
  .default_item{
    display: block;
    padding-top: 20px;
    width:90%;
    height: 60px;
    border-style: solid;
    border-width: 1px;
  }
  .card_box{
    float: left;

    list-style: none;
    width: 25%;
    padding: 0px;
  }
  .card_box li{
    float: left;
    width: 100px;
    border: solid 2px;
  }
</style>
