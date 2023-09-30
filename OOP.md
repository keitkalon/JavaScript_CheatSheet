# Classes in Javascript
```JavaScript
const badWords = [];

class Player {
  #isCaptain = false;
  static description = "Player"; // property of a class an not of an instance
  score = 0;
  power = 10;
  #slogan = "BOOOYAH"
  #id =  "795875" // private
  constructor(first, last){
     this.first = first;
     this.last = last;
  }
  static random(){ // method of a class
     return new Player("Unknown","Anonymous");
  }
  shouted() {
     console.log(`${this.first.toUpperCase()} ${this.slogan.toUpperCase()}!!!`);
  }
  tired () {
     this.power -= 1;
  }
  getId(){
     return this.#id;
  }
  #internalMethod(){ // private method
     return "Secret";
  }
  get fullname(){ // getter
     return this.first + " " + this.last;
  }
  set slogan(value){ // setter
     if(!badWords.includes(value) ){
        #slogan = values;
     } else{
        throw new Error("No bad words")
     };
  }
}

class Captain extends Player {
  players = [];
  constructor(first, last, players) {
    super(first, last);
    this.#isCaptain = true;
    this.players = players;
  }
}

const player1 = new Player("John","McUp")
const player2 = new Player("Ian","McDown")
const player3 = new Captain("Andy","McCaptain", [player1, player2])


player1.shouted();
player2.shouted();
console.log(player3)
                          
```
