<template>
   <div class="test">
      <h1 v-once>{{ story }}</h1>
      <h1>{{ story }}</h1>
      <input type="text" v-model="story" />
      <br />
      <hr>
      <button v-on:click="addClass">Change Btn</button>

      <p :class="[dispNum? 'colorB' : 'colorA']" >
         Lorem ipsum dolor sit amet consectetur adipisicing elit. Optio autem, provident perspiciatis placeat, saepe enim nostrum aspernatur quisquam eum harum quas eveniet sequi tempora exercitationem, illum odit nemo laboriosam quo!
      </p>

      <button v-on:click="borderArea">Border Settings</button>

      <h5>{{ bimp ? 'The button is Inactive' : 'The button is active' }}</h5>
      <button :disabled="bimp" :class="[ bimp? 'none' : 'meToo' ]">Fancy Btn</button>

      <div :style="{ background: bgColor, width: bgWidth, height: bgHeight, marginBottom: mgBtm }"></div>
   </div>
</template>


<script>
  export default {
    name: 'test',
    props: ['borderArea'],
    data() {
      return {
        story: 'Hi my name is Etinosa',
        dispNum: false,
        bimp: true,
        bgColor: 'yellow',
        bgWidth: '100%',
        bgHeight: '35px',
        mgBtm: '10px'
      }
    },

    methods: {
      addClass() {
        const h1 = document.querySelectorAll('h1');
        const h1Arr = Array.from(h1)

        h1Arr.forEach(cur => {
          cur.classList.toggle('backGrund')
        })
        // h1.classList.toggle('backGrund')

        if (h1Arr[0].className.includes('backGrund')) {
          this.dispNum = true;
          this.bimp = false;
        } else {
          this.dispNum = false;
          this.bimp = true;
        }
      }
    }
  }
</script>


<style scoped>
  .test {
    text-align: center;
  }

  h1 {
    text-shadow: 1px 1px 5px #08050594;
  }

  .backGrund {
    color: green;
  }

  .colorA {
    color: black;;
    background: orange;
  }

  .colorB {
    color: chocolate;
    background: blueviolet;
  }

  .meToo {
    background: pink;
  }
</style>