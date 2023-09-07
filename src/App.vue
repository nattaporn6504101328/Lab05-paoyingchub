<template>
  <div class="container">
    <h1>เกมเป่ายิ้งฉุบ!!!</h1>
    <div class="players">
      <div class="player">
        <p>ผู้เล่น: {{ player1Choice }}</p>
        <br>
        <img v-if="player1Choice === 'ค้อน'" src="https://www.lottoup99.com/wp-content/plugins/lottoup-paoyingchub-plugin/template/images/rock.png" alt="ค้อน" />
        <img v-if="player1Choice === 'กรรไกร'" src="https://www.lottoup99.com/wp-content/plugins/lottoup-paoyingchub-plugin/template/images/sci.png" alt="กรรไกร" />
        <img v-if="player1Choice === 'กระดาษ'" src="https://www.lottoup99.com/wp-content/plugins/lottoup-paoyingchub-plugin/template/images/paper.png" alt="กระดาษ" />
        <img v-if="player1Choice === 'ความรักชนะทุกอย่าง'" src="https://st3.depositphotos.com/12227958/34740/v/450/depositphotos_347400312-stock-illustration-sign-mini-heart-isolate-white.jpg" alt="ความรักชนะทุกอย่าง" />

        <br>
        <p>คะแนน: {{ player1Score }}</p>
      </div>
      <div class="player">
        <p>คอมพิวเตอร์: {{ player2Choice }}</p> <br>
        <img v-if="player2Choice === 'ค้อน'" src="https://www.lottoup99.com/wp-content/plugins/lottoup-paoyingchub-plugin/template/images/rock.png" alt="ค้อน" />
        <img v-if="player2Choice === 'กรรไกร'" src="https://www.lottoup99.com/wp-content/plugins/lottoup-paoyingchub-plugin/template/images/sci.png" alt="กรรไกร" />
        <img v-if="player2Choice === 'กระดาษ'" src="https://www.lottoup99.com/wp-content/plugins/lottoup-paoyingchub-plugin/template/images/paper.png" alt="กระดาษ" />
        <img v-if="player2Choice === 'ความรักชนะทุกอย่าง'" src="https://st3.depositphotos.com/12227958/34740/v/450/depositphotos_347400312-stock-illustration-sign-mini-heart-isolate-white.jpg" alt="ความรักชนะทุกอย่าง" />

        <br>
        <p>คะแนน: {{ player2Score }}</p>
      </div>
    </div>
    <div class="buttons">
      <button @click="startGame">เป่ายิ้งฉุบบบบ</button>
      <button @click="resetGame">เริ่มใหม่</button>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';

const imgUrls = [
  'https://www.lottoup99.com/wp-content/plugins/lottoup-paoyingchub-plugin/template/images/paper.png',
  'https://www.lottoup99.com/wp-content/plugins/lottoup-paoyingchub-plugin/template/images/sci.png',
  'https://www.lottoup99.com/wp-content/plugins/lottoup-paoyingchub-plugin/template/images/rock.png',
  'https://st3.depositphotos.com/12227958/34740/v/450/depositphotos_347400312-stock-illustration-sign-mini-heart-isolate-white.jpg'
];

const imgUrl = ref('');

const rd = Math.floor(Math.random() * imgUrls.length);
imgUrl.value = imgUrls[rd];


export default {
  data() {
    return {
      player1Choice: "",
      player2Choice: "",
      player1Score: 0,
      player2Score: 0,
      imgUrl: imgUrl,
    };
  },
  methods: {
    startGame() {
    const choices = ["ค้อน", "กรรไกร", "กระดาษ", "ความรักชนะทุกอย่าง"];
    this.player1Choice = choices[Math.floor(Math.random() * choices.length)];
    this.player2Choice = choices[Math.floor(Math.random() * choices.length)];

    if (this.player1Choice === this.player2Choice) {
      // เสมอกัน
    } else if (
      (this.player1Choice === "ค้อน" && (this.player2Choice === "กรรไกร" || this.player2Choice === "ความรักชนะทุกอย่าง")) ||
      (this.player1Choice === "กรรไกร" && (this.player2Choice === "กระดาษ" || this.player2Choice === "ความรักชนะทุกอย่าง")) ||
      (this.player1Choice === "กระดาษ" && (this.player2Choice === "ค้อน" || this.player2Choice === "ความรักชนะทุกอย่าง"))
    ) {
      this.player1Score++;
    } else if (
      (this.player2Choice === "ค้อน" && (this.player1Choice === "กรรไกร" || this.player1Choice === "ความรักชนะทุกอย่าง")) ||
      (this.player2Choice === "กรรไกร" && (this.player1Choice === "กระดาษ" || this.player1Choice === "ความรักชนะทุกอย่าง")) ||
      (this.player2Choice === "กระดาษ" && (this.player1Choice === "ค้อน" || this.player1Choice === "ความรักชนะทุกอย่าง"))
    ) {
      this.player2Score++;
    }

    if (this.player1Score > this.player2Score) {
      this.player1Choice = "ความรักชนะทุกอย่าง"; // ถ้าผู้เล่น 1 ชนะ
    } else if (this.player2Score > this.player1Score) {
      this.player2Choice = "ความรักชนะทุกอย่าง"; // ถ้าคอมพิวเตอร์ชนะ
    } else {
      this.player1Choice = ""; // ถ้าเสมอกัน
      this.player2Choice = "";
    }
  },
  resetGame() {
    this.player1Choice = "";
    this.player2Choice = "";
    this.player1Score = 0;
    this.player2Score = 0;
  },
},
    }
</script>

<style scoped>
  .container {
    text-align: center;
    font-size: 20px;
  }
  .players {
    display: flex;
    justify-content: space-around;
    margin: 50px;
    
  }
  .player {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: 50px;
  }
  img {
    width: 150px;
    height: 150px;
    border-radius: 5%;
  }
  .buttons {
    margin-top: 25px;
  border-radius: 1%;
  color: white; 
  font-size: 18px;
}

</style>
