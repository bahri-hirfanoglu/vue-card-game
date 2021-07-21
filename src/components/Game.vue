<template>
  <div class="game">
    <div class="cards" v-show="IsGame">
      <transition-group name="game_load" mode="out-in">
        <app-card
          v-for="(card, index) in card_data"
          :key="card.id"
          :cardimage="card.IsOpen == true ? card.image : DefaultCard"
          v-show="IsGame"
          @click.native="clickCard(index)"
        ></app-card>
      </transition-group>
    </div>
    <div class="menu" v-show="!IsGame">
      <app-menu @startGame="createGame"></app-menu>
    </div>
    <div class="table" v-show="IsGame">
      <table>
        <tr>
          <td>Claim: {{ player.claim }}</td>
          <td>True: {{ player.trueCount }}</td>
        </tr>
      </table>
    </div>
  </div>
</template>
<script>
import Card from "./Card.vue";
import Menu from "./Menu.vue";
export default {
 components: {
        appCard: Card,
        appMenu: Menu,
    },
    data: function() {
        return {
            card_data: [{
                    id: 1,
                    cardID: 1,
                    image: "./src/assets/cards/1.png",
                    IsOpen: false,
                    IsTrue: false,
                },
                {
                    id: 2,
                    cardID: 2,
                    image: "./src/assets/cards/2.png",
                    IsOpen: false,
                    IsTrue: false,
                },
                {
                    id: 3,
                    cardID: 3,
                    image: "./src/assets/cards/3.png",
                    IsOpen: false,
                    IsTrue: false,
                },
                {
                    id: 4,
                    cardID: 4,
                    image: "./src/assets/cards/4.png",
                    IsOpen: false,
                    IsTrue: false,
                },
                {
                    id: 5,
                    cardID: 5,
                    image: "./src/assets/cards/5.png",
                    IsOpen: false,
                    IsTrue: false,
                },
                {
                    id: 6,
                    cardID: 6,
                    image: "./src/assets/cards/6.png",
                    IsOpen: false,
                    IsTrue: false,
                },
                {
                    id: 7,
                    cardID: 7,
                    image: "./src/assets/cards/7.png",
                    IsOpen: false,
                    IsTrue: false,
                },
                {
                    id: 8,
                    cardID: 8,
                    image: "./src/assets/cards/8.png",
                    IsOpen: false,
                    IsTrue: false,
                },
                {
                    id: 9,
                    cardID: 1,
                    image: "./src/assets/cards/1.png",
                    IsOpen: false,
                    IsTrue: false,
                },
                {
                    id: 10,
                    cardID: 2,
                    image: "./src/assets/cards/2.png",
                    IsOpen: false,
                    IsTrue: false,
                },
                {
                    id: 11,
                    cardID: 3,
                    image: "./src/assets/cards/3.png",
                    IsOpen: false,
                    IsTrue: false,
                },
                {
                    id: 12,
                    cardID: 4,
                    image: "./src/assets/cards/4.png",
                    IsOpen: false,
                    IsTrue: false,
                },
                {
                    id: 13,
                    cardID: 5,
                    image: "./src/assets/cards/5.png",
                    IsOpen: false,
                    IsTrue: false,
                },
                {
                    id: 14,
                    cardID: 6,
                    image: "./src/assets/cards/6.png",
                    IsOpen: false,
                    IsTrue: false,
                },
                {
                    id: 15,
                    cardID: 7,
                    image: "./src/assets/cards/7.png",
                    IsOpen: false,
                    IsTrue: false,
                },
                {
                    id: 16,
                    cardID: 8,
                    image: "./src/assets/cards/8.png",
                    IsOpen: false,
                    IsTrue: false,
                },
            ],
            selected_card: [],
            IsGame: false,
            IsGameOver: false,
            DefaultCard: "./src/assets/card.png",
            animated: false,
            player: {
                claim: 20,
                trueCount: 0,
            },
        };
    },
    methods: {
        createGame: function() {
            for (let i = this.card_data.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [this.card_data[i], this.card_data[j]] = [
                    this.card_data[j],
                    this.card_data[i],
                ];
            }
            this.IsGame = true;
        },
        clickCard: function(value) {
            var card = this.card_data[value];
            if (
                this.player.claim > 0 &&
                this.card_data.find((el) => el.IsTrue == false)
            ) {
                if (!card.IsOpen && !card.IsTrue) {
                    if (this.selected_card.length < 2) {
                        this.player.claim--;
                        this.selected_card.push(card);
                        card.IsOpen = true;
                        if (this.selected_card.length == 2) {
                            if (
                                this.selected_card[0].cardID == this.selected_card[1].cardID
                            ) {
                                let first = this.card_data.find(
                                    (el) => el.id == this.selected_card[0].id
                                );
                                if (first) {
                                    first.IsTrue = true;
                                }
                                let second = this.card_data.find(
                                    (el) => el.id == this.selected_card[1].id
                                );
                                if (second) {
                                    second.IsTrue = true;
                                }
                                this.player.claim++;
                                this.player.trueCount++;
                            }
                            setTimeout(this.showCard, 1600);
                        }
                        if (
                            !this.card_data.find((el) => el.IsTrue == false) ||
                            this.player.claim <= 0
                        ) {
                             this.gameOver();
                        }
                    }
                }
            } else {
               this.gameOver();
            }
        },
        showCard: function(state = true) {
            for (var i in this.card_data) {
                if (this.card_data[i].IsOpen == state && !this.card_data[i].IsTrue) {
                    this.card_data[i].IsOpen = !state;
                }
            }
            this.selected_card = [];
        },
        gameOver: function() {
            let compname = "app-win";
            if (this.player.claim <= 0) {
                if (this.player.trueCount == this.card_data.length / 2) {
                    compname = "app-win";
                } else {
                    compname = "app-lose";
                }
            } else {
                if (this.player.trueCount == this.card_data.length / 2) {
                    compname = "app-win";
                }
            }
            this.$emit("gameOver", compname);
        },
    },
};
</script>

<style lang="sss" scoped>
.game {
  width: 800px;
  height: 600px;
  margin: auto;
  position: relative;
  margin-top: 40px;
}
.cards {
  width: 460px;
  height: 475px;
  background: hsl(240deg 7% 97%);
  margin: auto;
  box-shadow: 0 0.4rem 2rem hsl(230deg 65% 56%);
  position: relative;
}
.menu {
  width: 100%;
  height: 200px;
  margin-top: 10px;
}

td {
  border: 1px solid #ddd;
  padding: 8px;
}
.table {
  width: 100%;
  margin-top: 90px;
}
.game_load-enter-active {
  animation: game_load ease-in-out 1.5s forwards;
}

@keyframes game_load {
  from {
    transform: rotateY(0);
  }
  to {
    transform: rotateY(1080deg);
  }
}
</style>