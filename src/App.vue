<template>
  <div class="main-wrap flex flex-col h-[100vh] overflow-hidden">
    <header
      class="z-1 flex h-7 w-full items-center justify-between rounded-t-[4px] bg-gradient-to-b from-[#FDFDFD] via-[#EAEAEA] to-white px-2 shadow-[0px_2px_10px_3px_rgba(0,0,0,0.25),inset_0px_1px_0px_0px_rgba(255,255,255,0.40),inset_0px_-1px_0px_0px_rgba(0,0,0,0.1)]">
      <div class="flex items-center">
        <a class="h-6 p-1 hover:bg-black/10" href="/"><img alt="Succinct Logo" width="12" height="12" decoding="async"
            data-nimg="1" class="no-drag select-none" style="color: transparent"
            src="@/assets/images/succinct-icon-pink.svg" /></a><button
          class="items-center justify-center gap-2 whitespace-nowrap rounded-none font-medium ring-offset-background transition-colors focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2 disabled:pointer-events-none disabled:opacity-50 [&amp;_svg]:pointer-events-none [&amp;_svg]:size-4 [&amp;_svg]:shrink-0 text-neutral-900 hover:text-neutral-900/80 active:text-neutral-900/60 h-6 select-none px-2 py-0 text-sm hover:bg-black/5 data-[state=open]:bg-black/10 hidden sm:block"
          type="button" id="radix-:R6lfb:" aria-haspopup="menu" aria-expanded="false" data-state="closed">
          <p class="font-oracle">File</p>
        </button><button
          class="items-center justify-center gap-2 whitespace-nowrap rounded-none font-medium ring-offset-background transition-colors focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2 disabled:pointer-events-none disabled:opacity-50 [&amp;_svg]:pointer-events-none [&amp;_svg]:size-4 [&amp;_svg]:shrink-0 text-neutral-900 hover:text-neutral-900/80 active:text-neutral-900/60 h-6 select-none px-2 py-0 text-sm hover:bg-black/5 data-[state=open]:bg-black/10 hidden sm:block"
          type="button" id="radix-:R8lfb:" aria-haspopup="menu" aria-expanded="false" data-state="closed">
          <p class="font-oracle">Edit</p>
        </button><button
          class="items-center justify-center gap-2 whitespace-nowrap rounded-none font-medium ring-offset-background transition-colors focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2 disabled:pointer-events-none disabled:opacity-50 [&amp;_svg]:pointer-events-none [&amp;_svg]:size-4 [&amp;_svg]:shrink-0 text-neutral-900 hover:text-neutral-900/80 active:text-neutral-900/60 h-6 select-none px-2 py-0 text-sm hover:bg-black/5 data-[state=open]:bg-black/10 hidden sm:block"
          type="button" id="radix-:Ralfb:" aria-haspopup="menu" aria-expanded="false" data-state="closed">
          <p class="font-oracle">View</p>
        </button>
      </div>
      <div class="flex items-center">
        <div class="mr-2 flex gap-2 text-sm font-medium">
          <span class="hidden sm:block">Balance: </span>66.66<!-- -->
          Credits
        </div>
        <button
          class="justify-center whitespace-nowrap text-sm font-medium ring-offset-background transition-colors focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2 disabled:pointer-events-none disabled:opacity-50 [&amp;_svg]:pointer-events-none [&amp;_svg]:size-4 [&amp;_svg]:shrink-0 p-1 items-center gap-1 rounded-none px-1 hidden md:flex"
          type="button" id="radix-:R75fb:" aria-haspopup="menu" aria-expanded="false" data-state="closed">
          <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none"
            stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
            class="lucide lucide-battery-full">
            <rect width="16" height="10" x="2" y="7" rx="2" ry="2"></rect>
            <line x1="22" x2="22" y1="11" y2="13"></line>
            <line x1="6" x2="6" y1="11" y2="13"></line>
            <line x1="10" x2="10" y1="11" y2="13"></line>
            <line x1="14" x2="14" y1="11" y2="13"></line>
          </svg></button><button
          class="items-center justify-center gap-2 whitespace-nowrap text-sm font-medium ring-offset-background transition-colors focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2 disabled:pointer-events-none disabled:opacity-50 [&amp;_svg]:pointer-events-none [&amp;_svg]:size-4 [&amp;_svg]:shrink-0 p-1 rounded-none px-1 hidden md:flex"
          type="button" id="radix-:R95fb:" aria-haspopup="menu" aria-expanded="false" data-state="closed">
          <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none"
            stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
            class="lucide lucide-bluetooth">
            <path d="m7 7 10 10-5 5V2l5 5L7 17"></path>
          </svg></button><button
          class="inline-flex items-center justify-center gap-2 whitespace-nowrap text-sm font-medium ring-offset-background transition-colors focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2 disabled:pointer-events-none disabled:opacity-50 [&amp;_svg]:pointer-events-none [&amp;_svg]:size-4 [&amp;_svg]:shrink-0 p-1 rounded-none px-1"
          type="button" id="radix-:Rb5fb:" aria-haspopup="menu" aria-expanded="false" data-state="closed">
          <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none"
            stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
            class="lucide lucide-wifi">
            <path d="M12 20h.01"></path>
            <path d="M2 8.82a15 15 0 0 1 20 0"></path>
            <path d="M5 12.859a10 10 0 0 1 14 0"></path>
            <path d="M8.5 16.429a5 5 0 0 1 7 0"></path>
          </svg></button><button
          class="inline-flex items-center justify-center gap-2 whitespace-nowrap text-sm font-medium ring-offset-background transition-colors focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2 disabled:pointer-events-none disabled:opacity-50 [&amp;_svg]:pointer-events-none [&amp;_svg]:size-4 [&amp;_svg]:shrink-0 p-1 rounded-none px-1"
          type="button" id="radix-:Rd5fb:" aria-haspopup="menu" aria-expanded="false" data-state="closed">
          <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none"
            stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
            class="lucide lucide-volume-x">
            <path
              d="M11 4.702a.705.705 0 0 0-1.203-.498L6.413 7.587A1.4 1.4 0 0 1 5.416 8H3a1 1 0 0 0-1 1v6a1 1 0 0 0 1 1h2.416a1.4 1.4 0 0 1 .997.413l3.383 3.384A.705.705 0 0 0 11 19.298z">
            </path>
            <line x1="22" x2="16" y1="9" y2="15"></line>
            <line x1="16" x2="22" y1="9" y2="15"></line>
          </svg>
        </button>
        <p class="font-oracle ml-2 select-none text-sm">
          <span class="hidden md:inline">Thu 11:29 AM</span><span class="md:hidden">11:29 AM </span>
        </p>
      </div>
    </header>

    <main class="flex flex-1 justify-center">
      <MacOSWindow title="Operation Guide" :x="520" :width="360" :height="240">
        <a-list>
          <a-list-item>
            <span class="bdfont">⬆️⬇️⬅️➡️</span>: move.</a-list-item>
          <a-list-item><span class="bdfont">N</span>: start the game.</a-list-item>
          <a-list-item><span class="bdfont">S</span>: Turn off the background
            music.</a-list-item>
          <a-list-item><span class="bdfont">P</span>: Pause the game.</a-list-item>
        </a-list>
      </MacOSWindow>

      <MacOSWindow :x="520" :y="300" :width="360" :height="220">
        <a-row class="grid-demo" style="margin-bottom: 16px">
          <a-col flex="auto">
            <h1 class="text-center bdfont">
              <p class="text-[#fe11c5]">Succinct</p>
              Pacman <br />
              with <span class="text-blue-300">SP1</span><br />
              by freshguy
            </h1>
          </a-col>
        </a-row>
      </MacOSWindow>

      <MacOSWindow title="PACMAN" :x="900" :width="360" :height="550">
        <div id="pacman" class="mt-10 rounded-md overflow-hidden"></div>
        <div class="text-center">
          <a-button type="primary" status="danger" :disabled="proofLoading" @click="onProof">Proof(SP1)</a-button>
        </div>
      </MacOSWindow>

      <MacOSWindow title="Leaderboard" :x="1280" :y="220" :width="360" :height="600">
        <Leaderboard />
      </MacOSWindow>
    </main>

    <div class="z-12 flex h-16 justify-center">
      <div class="relative flex w-[85%] justify-between gap-3 border border-[#8C016C] p-2 md:w-[60%]" style="
          background-image: linear-gradient(
            180deg,
            rgba(198, 237, 255, 0.8) 23.36%,
            rgba(254, 17, 197, 0.8) 85.09%
          );
        ">
        <div class="flex items-center gap-3">
          <div class="hidden sm:flex sm:items-center sm:gap-3">
            <div class="relative mt-[1px] rounded-md overflow-hidden" data-state="closed">
              <a class="relative" href="#"><img alt="Ferris Volleyball" width="48" height="48" decoding="async"
                  data-nimg="1" class="no-drag select-none" style="color: transparent"
                  src="@/assets/images/pacman.jpg" /></a>
              <div
                class="absolute left-1/2 h-0 w-0 -translate-x-1/2 rotate-180 border-x-[4px] border-t-[4px] border-x-transparent border-t-black bottom-[-4px]">
              </div>
            </div>
          </div>
        </div>
        <div class="flex items-center gap-3">
          <div class="h-full w-[2px] rounded-full bg-gradient-to-b from-neutral-100 to-neutral-400"></div>
          <div class="relative -mt-[2px]" data-state="closed">
            <a class="relative" href="javascript:void(0)"><img alt="Trash" width="48" height="48" decoding="async"
                data-nimg="1" class="no-drag select-none" style="color: transparent"
                src="@/assets/images/trash-app.webp" /></a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref } from "vue";
import MacOSWindow from "./components/MacOSWindow.vue";
import Leaderboard from "./components/Leaderboard.vue";
import { Message, Modal } from "@arco-design/web-vue";
import "@arco-design/web-vue/es/message/style/css";
import "@arco-design/web-vue/es/modal/style/css";
import { client } from './utils/http'

onMounted(() => {
  var el = document.getElementById("pacman");

  const root = import.meta.env.PROD ? '/pacman-sp1/' : "./"

  window.setTimeout(function () {
    window.PACMAN.init(el, root);
  }, 0);
});

function stringToHex(str) {
    const encoder = new TextEncoder();
    const bytes = encoder.encode(str);

    const hexArray = Array.from(bytes, byte => 
        byte.toString(16).padStart(2, '0')
    );

    const hexString = hexArray.join('');

    return `0x${hexString}`;
}

const proofLoading = ref(false);

function onProof() {
  if (!window.localStorage.getItem("userName")) {
    const userStr = prompt("Please enter your name.") || "";

    window.localStorage.setItem("userName", userStr);
    return
  }

  const curr = window.PACMAN.user().theScore();

  if (curr <= 0) {
    Message.error("Please obtain some scores first.");
    return;
  }

  proofLoading.value = true;

  const rawjson = JSON.stringify({
    playerName: window.localStorage.getItem("userName"),
    score: curr,
    level: 1,
  })

  const startTime = performance.now();

  client
    .post(
      "/scores",
      {
        proof: stringToHex(rawjson).slice(2),
        public_inputs: stringToHex(Date.now()).slice(2),
        "vkey_hash": stringToHex(curr).slice(2),
        "mode": "groth16"
      }
    )
    .then((res) => {
      if (res.status === 200 || res.status === 201) {
        const endTime = performance.now();
        Modal.info({
          title: '',
          content: `Proof Success, MODE: groth16, took: ${endTime - startTime}ms`,
          okText: 'ok'
        })
      } else {
        Message.error("Proof fail");
      }
    })
    .finally(() => {
      proofLoading.value = false;
    });
}
</script>

<style scoped>
@font-face {
  font-family: "BDCartoonShoutRegular";
  src: url("@/assets/fonts/BD_Cartoon_Shout-webfont.ttf") format("truetype");
  font-weight: normal;
  font-style: normal;
}

#pacman {
  height: 430px;
  width: 342px;
  margin: 20px auto;
}

.main-wrap {
  background-image: url(@/assets/images/os-background-mini.jpg);
  background-size: cover;
  background-position: 50% center;
}

.bdfont {
  font-family: "BDCartoonShoutRegular";
}
</style>
