<script lang="ts">
   
    import { onMount } from "svelte";
    import { base } from '$app/paths';



    let currentText = '';
  let texts = [
                "Next in line? Always on time. Experience efficient and stress-free queuing today.", 
                "Transform long waits into seamless experiences with our intelligent queuing solution.", 
                "Say goodbye to chaos—our system organizes queues so you can focus on what matters most.", 
                "Revolutionizing how you wait—no stress, no hassle, just seamless service.",
              ]; 
  let textIndex = 0;


  
  function typeText() {
    if (textIndex < texts.length) {
      let text = texts[textIndex];
      let charIndex = 0;
      
      const typeInterval = setInterval(() => {
        currentText += text[charIndex];
        charIndex++;
        
        if (charIndex === text.length) {
          clearInterval(typeInterval);
          setTimeout(() => {
            currentText = ''; // Clear text for backspace effect
            textIndex = (textIndex + 1) % texts.length; // Move to the next text
            typeText();
          }, 2000); // Wait 2 second before backspacing
        }
      }, 30); // Speed of typing
    }
  }

  // Start typing animation on mount
  onMount(() => {
    typeText();
  });
</script>

<style>

@keyframes typing {
  0% {
    width: 0;
  }
  100% {
    width: 100%;
  }
}

@keyframes backspace {
  0% {
    width: 100%;
  }
  100% {
    width: 0;
  }
}

@keyframes blink-caret {
  from, to {
    border-color: transparent;
  }
  50% {
    border-color: white; /* Color of the cursor */
  }
}

  @keyframes move_wave {
    0% {
        transform: translateX(0) translateZ(0) scaleY(1)
    }
    50% {
        transform: translateX(-25%) translateZ(0) scaleY(0.55)
    }
    100% {
        transform: translateX(-50%) translateZ(0) scaleY(1)
    }
}


.waveWrapper {
    overflow: hidden;
    position: absolute;
    left: 0;
    right: 0;
    bottom: 0;
    top: 0;
    margin: auto;
    z-index: -10;
}
.waveWrapperInner {
    position: absolute;
    width: 100%;
    overflow: hidden;
    height: 100%;
    bottom: -1px;
    background-image: linear-gradient(to top, #0F2A1D 20%, #0F2A1D 80%);
}
.bgTop {
    z-index: 15;
    opacity: 0.5;
}
.bgMiddle {
    z-index: 10;
    opacity: 0.75;
}
.bgBottom {
    z-index: 5;
}
.wave {
    position: absolute;
    left: 0;
    width: 200%;
    height: 100%;
    background-repeat: repeat no-repeat;
    background-position: 0 bottom;
    transform-origin: center bottom;
}
.waveTop {
    background-size: 50% 100px;
}
.waveAnimation .waveTop {
  animation: move-wave 3s;
   -webkit-animation: move-wave 3s;
   -webkit-animation-delay: 1s;
   animation-delay: 1s;
}
.waveMiddle {
    background-size: 50% 120px;
}
.waveAnimation .waveMiddle {
    animation: move_wave 10s linear infinite;
}
.waveBottom {
    background-size: 50% 100px;
}
.waveAnimation .waveBottom {
    animation: move_wave 15s linear infinite;
}
</style>

<main>
    <div class="flex -z-10">
    <div class="waveWrapper waveAnimation">
        <div class="waveWrapperInner bgTop">
          <div class="wave waveTop" style="background-image: url('http://front-end-noobs.com/jecko/img/wave-top.png')"></div>
        </div>
        <div class="waveWrapperInner bgMiddle">
          <div class="wave waveMiddle" style="background-image: url('http://front-end-noobs.com/jecko/img/wave-mid.png')"></div>
        </div>
        <div class="waveWrapperInner bgBottom">
          <div class="wave waveBottom" style="background-image: url('http://front-end-noobs.com/jecko/img/wave-bot.png')"></div>
        </div>
      </div>
    </div>

    <section id="introPage" class="mt-10 grid grid-cols-1 lg:grid-cols-2 gap-5 lg:gap-x-0 py-sm:py-0">
        <div class="flex flex-col lg:justify-center text-center lg:text-left lg:pl-10 gap-8 md:gap-10 lg:gap-8">
            <h2 class="font-semibold text-5xl text-white sm:text-6xl md:text-6xl">
                Queueing<span class="text-yellow-200"> <br> Monitoring System</span>
            </h2>
            <div class="relative">
                <p class="text-base text-white sm:text-lg md:text-xl typing-text absolute top-0 left-0">
                    {currentText}
                </p>
            </div>
            <a href="{base}/Queue" class="block">
                <button class="mt-12 mx-auto lg:mr-auto lg:ml-0 text-base sm:text-lg md:text-xl poppins relative overflow-hidden px-6 py-3 group rounded-full bg-white text-green-950">
                    <div class="absolute top-0 right-full w-full h-full bg-amber-300 opacity-20 group-hover:translate-x-full z-0 duration-200"></div>
                    <h4 class="relative z-9">Get Number &rarr;</h4>
                </button>
            </a>
        </div>
        
        <div class="relative place-items-center">
            <div class="relative max-h-[70vh]">
                <img src="assets/queue2.png" alt="Jenishe Salem" class="object-cover z-[1] max-h-[60vh]" />
                <!-- <img src="assets/images/butterfly.png" alt="Jenishe Salem" class="object-cover z-[2] max-h-[70vh] absolute top-0 left-0 animate-wiggle" /> -->
            </div>            
        </div>
    </section>
  
</main>