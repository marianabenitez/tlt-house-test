<template>
  <v-container>
    <v-card v-show="!completed">
      <v-card-title>Select 5 items from the list below</v-card-title>
      <v-flex v-for="(item, index) in items" :key="items[index].text">
        <!--[:disabled] EXPLANATION: disable current checkbox if it's unselected and there are 5+ selected checkboxes-->
        <v-checkbox
          class="c-box"
          :label="item.text"
          v-model="item.selected"
          :disabled="
            items.filter((i) => i.selected).length >= 5 &&
              !items[items.indexOf(item)].selected
          "
          @change="sumHousePoints"
        >
        </v-checkbox>
      </v-flex>
      <v-btn
        class="s-btn"
        color="primary"
        :disabled="items.filter((i) => i.selected).length < 5"
        @click="confirm"
      >
        CONFIRM
      </v-btn>
    </v-card>
    <v-card id="results" v-show="completed">
      <v-card-title>Results</v-card-title>
      <p class="c-box">{{ sum[0] }} >> Second House</p>
      <p class="c-box">{{ sum[1] }} >> Third House</p>
      <p class="c-box">{{ sum[2] }} >> Fourth House</p>
      <p class="c-box">{{ sum[3] }} >> Fifth House</p>
      <p class="c-box">{{ sum[4] }} >> Sixth House</p>
      <p class="c-box">{{ sum[5] }} >> Seventh House</p>
      <p class="c-box">{{ sum[6] }} >> Eighth House</p>
      <p class="c-box">{{ sum[7] }} >> Ninth House</p>
      <v-btn class="s-btn" color="primary" @click="copy">
        COPY
      </v-btn>
    </v-card>
  </v-container>
</template>

<script>
export default {
  name: "Main",
  mounted() {},
  methods: {
    confirm() {
      this.completed = true;
    },
    copy() {
      let r = document.querySelector("#results");
      let nodes = r.querySelectorAll(".c-box");
      let text = "";
      nodes.forEach((n) => {
        text += n.textContent + "\r\n";
      });

      this.copyToClipboard(text);
    },
    sumHousePoints() {
      let result = [0, 0, 0, 0, 0, 0, 0, 0];
      this.items.forEach((item) => {
        if (item.selected) {
          result = this.arraySum(result, item.housePoints);
        }
      });
      this.sum = result;
    },
    copyToClipboard(text){
      var clipboard = document.createElement("textarea");
      document.body.appendChild(clipboard);
      clipboard.value = text;
      clipboard.select();
      document.execCommand("copy");
      document.body.removeChild(clipboard);
    },
    arraySum(array1, array2) {
      // provided by https://www.w3resource.com/javascript-exercises/javascript-array-exercise-19.php
      let result = [];
      let count = 0;
      let i = 0;

      while (count < array1.length && count < array2.length) {
        result.push(array1[count] + array2[count]);
        count++;
      }

      if (count === array1.length) {
        for (i = count; i < array2.length; i++) {
          result.push(array2[i]);
        }
      } else {
        for (i = count; i < array1.length; i++) {
          result.push(array1[i]);
        }
      }

      return result;
    },
  },
  data() {
    return {
      completed: false,
      sum: [0, 0, 0, 0, 0, 0, 0, 0],
      items: [
        {
          text: "A sack of ossicles",
          selected: false,
          housePoints: [0, 0, 0, 0, 0, 0, 0, 15],
        },
        {
          text: "A sack of fresh human hands",
          selected: false,
          housePoints: [5, 10, 5, 5, 6, 7, 5, 5],
        },
        {
          text:
            "A rolled-up flag of the Cohort, soldiers of the blessed Necrolord Prime",
          selected: false,
          housePoints: [15, 1, 1, 1, 1, 5, 1, 1],
        },
        {
          text: "Pen and  flimsy",
          selected: false,
          housePoints: [0, 0, 0, 10, 15, 10, 10, 0],
        },
        {
          text: "A bottle of 160 proof rum",
          selected: false,
          housePoints: [1, 15, 5, 0, 0, 0, 0, 0],
        },
        {
          text:
            "A  waterproof portrait of the Emperor, here portrayed as the Merciful Resurrector",
          selected: false,
          housePoints: [0, 0, 0, 0, 0, 5, 15, 5],
        },
        {
          text: "An empty bottle with a lid to seal it",
          selected: false,
          housePoints: [0, 0, 0, 9, 9, 0, 9, 0],
        },
        {
          text: "An antique flare gun of curious make",
          selected: false,
          housePoints: [0, 0, 15, 5, 5, 0, 0, 0],
        },
        {
          text: "A book of antiquated Ninth House prayers",
          selected: false,
          housePoints: [0, 0, 0, 1, 5, 5, 0, 15],
        },
        {
          text: "A twenty-five litre container of BLOOD!!!!",
          selected: false,
          housePoints: [0, 0, 0, 9, 0, 0, 0, 0],
        },
        {
          text: "A single sharp rapier",
          selected: false,
          housePoints: [10, 2, 9, 0, 0, 9, 0, 0],
        },
        {
          text: "A shaving mirror",
          selected: false,
          housePoints: [0, 2, 6, 0, 0, 0, 0, 0],
        },
        {
          text: "A case of absolutely disgusting army rations, hard and bad",
          selected: false,
          housePoints: [9, 1, 1, 1, 1, 1, 1, 1],
        },
        {
          text: "A case of extremely glamorous luxe rations, but poisoned",
          selected: false,
          housePoints: [0, 8, 0, 0, 0, 0, 5, 0],
        },
        {
          text: "A  tinier, leakier fold-out raft, with a dubious motor",
          selected: false,
          housePoints: [0, 0, 5, 0, 0, 0, 0, 0],
        },
      ],
    };
  },
};
</script>

<style scoped>
.c-box {
  margin-left: 3vh;
  margin-top: -1.5vh;
}
.s-btn {
  margin-left: 3vh;
  margin-bottom: 3vh;
}
</style>
