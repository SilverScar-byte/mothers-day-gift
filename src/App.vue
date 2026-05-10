<template>
  <div class="app">
    <!-- Back Button -->
    <button v-if="opened" class="back-btn" @click="closeLetter">
      ← Back
    </button>

    <!-- Greeting PNG -->
    <img
      v-if="opened"
      src="/greeting.png"
      class="greeting"
      alt="Happy Mother's Day"
    />

    <!-- Envelope -->
    <img
      v-if="!opened"
      src="/envelope.png"
      class="envelope"
      @click="openEnvelope"
      alt="Envelope"
    />

    <!-- Letter -->
    <div v-if="opened" class="letter-container">
      <img src="/letter.png" class="letter-bg" />

      <div class="letter-text">
        <p>
          First of all, a Happy Mothers’ Day to one of, if not the, strongest woman I know.
          Your strength has carried us, your family, through situations that are beyond imaginable yet you still thrived and even got us out of it.
        </p>

        <p>
          You’re the reason why our lives are as good as it is now and why it keeps on getting better.
          Thank you for everything, Ma. For being the leg of this family, the walls, the light, and the pillars.
        </p>

        <p>
          Thank you for raising us despite being hard-headed kids and thank you for always supporting us –
          even if your work does not allow you and sometimes you doubt it.
        </p>

        <p>
          I’m thankful that I was born as your child and I will always be thankful that you are my mom.
          I am me because of you, even if not fully.
        </p>

        <p>
          You’re always in my prayers, Ma. God knows how much I’ve cried just thinking of you and wanting to help you.
        </p>

        <p>
          Babawi din ako, yayaman ang anak mo. I will give back what you lost during your sacrifices, Ma.
        </p>

        <p style="margin-top: 18px; font-weight: bold;">
          I love you po!<br />
          — Echo
        </p>
      </div>
    </div>

    <!-- Flowers -->
    <img v-if="opened" src="/flower1.png" class="flower f1" />
    <img v-if="opened" src="/flower2.png" class="flower f2" />
    <img v-if="opened" src="/flower3.png" class="flower f3" />
  </div>
</template>

<script setup>
import { ref } from "vue";

const opened = ref(false);

// sound effects
const openSound = new Audio("/sounds/open.mp3");

// background music
const bgMusic = new Audio("/music/warm-memories.mp3");
bgMusic.loop = true;
bgMusic.volume = 1;

function openEnvelope() {
  openSound.currentTime = 0;
  openSound.play();

  bgMusic.currentTime = 0;
  bgMusic.play();

  opened.value = true;
}

function closeLetter() {
  bgMusic.pause();
  bgMusic.currentTime = 0;

  opened.value = false;
}
</script>

<style>
@font-face {
  font-family: "Moistly Vengions";
  src: url("/fonts/MoistlyVengionsDemo-Regular.otf") format("opentype");
}

.app {
  position: fixed;
  inset: 0;
  background: linear-gradient(135deg, #1e90ff, #4facfe, #8fd3ff, #ffffff);
  display: flex;
  justify-content: center;
  align-items: center;
  overflow: hidden;
}

/* Back button */
.back-btn {
  position: absolute;
  top: 20px;
  left: 20px;

  background: rgba(255, 255, 255, 0.6);
  border: none;
  padding: 8px 14px;
  border-radius: 10px;

  font-size: 14px;
  font-family: "Moistly Vengions", serif;
  color: #333;

  cursor: pointer;
  transition: all 0.3s ease;
  z-index: 10;
}

.back-btn:hover {
  background: rgba(255, 255, 255, 0.9);
  transform: translateY(-2px);
}

/* Greeting image (top-right) */
.greeting {
  position: absolute;
  top: 100px;
  right: 100px;

  width: min(520px, 55vw);
  height: auto;

  z-index: 10;
  pointer-events: none;

  animation: fadeIn 0.6s ease;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(-10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Envelope */
.envelope {
  width: min(80vw, 800px);
  cursor: pointer;
  transition: transform 0.3s ease;
}

.envelope:hover {
  transform: translateY(-10px);
}

/* Letter */
.letter-container {
  position: relative;
  width: min(90vw, 850px);
  animation: pop 0.5s ease;
}

.letter-bg {
  width: 100%;
  display: block;
}

/* Text */
.letter-text {
  position: absolute;
  top: 50%;
  left: 50%;
  width: 55%;
  max-height: 80%;
  transform: translate(-50%, -50%);
  overflow: hidden;

  font-family: "Moistly Vengions", serif;
  font-size: 16px;
  color: #2c2c2c;
  line-height: 1.8;
  text-align: justify;
}

/* FLOWERS */
.flower {
  position: absolute;
  pointer-events: none;
  animation: pop 0.6s ease;
}

.f2 {
  top: 0%;
  left: 0%;
  width: 500px;
}

.f3 {
  bottom: 3%;
  right: 3%;
  width: 300px;
}

.f1 {
  bottom: 5%;
  left: 12%;
  width: 500px;
}

/* Pop animation */
@keyframes pop {
  from {
    transform: scale(0.6);
    opacity: 0;
  }
  to {
    transform: scale(1);
    opacity: 1;
  }
}

/* 📱 MOBILE RESPONSIVE FIX */
@media (max-width: 768px) {

  /* Greeting */
  .greeting {
    top: 40px;
    right: 20px;
    width: 220px;
  }

  /* Envelope */
  .envelope {
    width: 85vw;
  }

  /* Letter container */
  .letter-container {
    width: 95vw;
  }

  /* Letter text */
  .letter-text {
    width: 70%;
    font-size: 12px;
    line-height: 1.5;
  }

  /* Flowers scale down */
  .f1 {
    width: 220px;
    left: 5%;
    bottom: 3%;
  }

  .f2 {
    width: 220px;
  }

  .f3 {
    width: 180px;
    right: 2%;
    bottom: 2%;
  }

  /* Back button smaller */
  .back-btn {
    font-size: 12px;
    padding: 6px 10px;
  }
}
</style>