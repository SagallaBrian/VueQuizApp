<template>
  <div>
    <b-container fluid="lg text-secondary">
      <h5 class="font-weight-normal text-success">
        Welcome To {{ Contmessage }}
      </h5>
      <div class="p-2"></div>

      <!-- <b-card class="" v-for="item in messagevar" :key="item.correct_answer">
                  <h5 class="font-weight-normal text-secondary">
                    {{item.question}}
                  </h5>
                  <h6 class="font-weight-normal text-success">
                    {{item.correct_answer}}
                  </h6>
              </b-card> -->

      <b-card>
        <div class="row justify-content-center">
          <div class="col-md-8 text-center">
            <div class="text-secondary pt-4" v-if="messagevar[questindex]">
              <h5 class="font-weight-normal text-secondary">
                {{ messagevar[questindex].question }}
              </h5>

              <div class="p-2"></div>

              <h6 class="font-weight-normal">
                Click on The Correct Answer (Once You Click You cannot redo)
              </h6>

              <div class="">
                <b-list-group>
                  <b-list-group-item
                    v-for="oneitem in tricomp"
                    v-on:click="selectedind(oneitem)"
                    :disabled="!forlistg"
                    :key="oneitem"
                    :class="[
                      storecorectans === oneitem ? 'corectstyle' : '',
                      selectedans === oneitem && storecorectans !== oneitem
                        ? 'incorecstyle'
                        : '',
                    ]"
                  >
                    {{ oneitem }}</b-list-group-item
                  >

                  <!-- <b-list-group-item >The answer is: {{ messagevar[questindex].correct_answer }}</b-list-group-item> -->
                </b-list-group>
                <div class="pt-2 text-dark">
                  <b>{{ forcorestion }}</b>
                  <h5>Marks {{ nofCorrect }}/ 10</h5>
						<h5>{{finalscore}}</h5>
                </div>
              </div>

              <div class="p-4">
                <!-- <button class="btn btn-primary" v-on:click="drcbtn">Previous</button> &nbsp; -->
                <button
                  class="btn btn-primary"
                  :disabled="!checkind"
                  v-on:click="indrbtn"
                >
                  Next
                </button>
                <!-- <button class="btn btn-danger" v-on:click="ansfunc">Next</button> :class="{changestyle: ifcorrect}" -->
              </div>
            </div>

            <div class="text-secondary pt-4 pb-2" v-else>
              <h4 class="font-weight-normal">Loading ....</h4>
            </div>
          </div>
        </div>
      </b-card>
    </b-container>

    <!-- 
              https://vegibit.com/vue-js-express-tutorial/ 
              https://opentdb.com/api.php?amount=10&category=18&type=multiple 
              https://www.youtube.com/watch?v=4deVCNJq3qc&t=2916s  
            -->
  </div>
</template>

<script>
export default {
  name: "Content",
  props: {
    Contmessage: {
      type: String,
      default: "Online Tech quiz",
    },
    contindex: {
      type: Number,
      default: 0,
    },
  },
  data: function () {
    return {
      messagevar: [],
      questindex: 0,
      checkind: false,
      forlistg: true,
      forcorestion: "",
      finalscore: "",

      //for select function
      selectedans: "",
      storecorectans: "",
      nofCorrect: 0,
      noinCorrect: 1,
    };
  },
  mounted() {
    fetch("https://opentdb.com/api.php?amount=10&category=18&type=multiple", {
      method: "get",
    })
      .then((response) => response.json())
      .then((result) => {
        this.messagevar = result.results;
      });
  },
  computed: {
    tricomp() {
      var impor = this.messagevar[this.questindex]["incorrect_answers"];
      var corect = this.messagevar[this.questindex]["correct_answer"];
      impor.push(corect);
      // return this.messagevar[this.questindex][this.forincor]
      return impor.sort();
    },
  },

  methods: {
    indrbtn: function () {
      this.forlistg = true;
      this.questindex += 1;
      this.checkind = false;
      this.forcorestion = "";
      if (this.questindex == 9) {
      //   console.log("hey there");
        this.checkind = false;
		}
		
    },

    // drcbtn: function () {
    //   this.questindex -= 1;
    // },

    selectedind: function (fooneitem) {
      this.selectedans = fooneitem;
		this.forlistg = false;
		this.checkind = true;
		this.noinCorrect += 1
		// console.log(fooneitem);
		
		

      var corect = this.messagevar[this.questindex]["correct_answer"];
      this.storecorectans = this.messagevar[this.questindex]["correct_answer"];

      if (corect == this.selectedans) {
      //   console.log(this.selectedans);
        this.nofCorrect += 1;
        this.forcorestion = "That is Correct ";
      } else {
        this.forcorestion = "That is Inccorect. The answer is " + corect;
		}
		
		if(this.noinCorrect ==11)
		{
			this.finalscore = "That is All Your Final Score Is: " + this.nofCorrect *10 +"%";
			this.checkind = false;
		}

      // this.selectedans = ""
      // this.storecorectans = ""
    },
  },
};
</script>

<style scoped>
.jjjjh3 {
  margin: 40px 0 0;
}
.kkkkul {
  list-style-type: none;
  padding: 0;
}
.jjjli {
  display: inline-block;
  margin: 0 10px;
}
.corectstyle {
  background-color: #42b983;
  color: #ffffff;
}
.incorecstyle {
  background-color: #b94242;
  color: #ffffff;
}
</style>
