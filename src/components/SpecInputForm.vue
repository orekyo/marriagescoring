<template>
  <h1>婚活戦闘力診断</h1>
  <p class="read-the-docs">婚活戦闘力の計算方法はアイコンのリンク先のブログを参照</p>
  <div>
    <fieldset>診断者ニックネーム：<input type="text" v-model="nickname" /></fieldset>

    <fieldset>
      <span>診断者の性別：</span>
      <span>
        <input type="radio" id="man" name="sex" value="man" v-model="sex" checked>
        <label for="man">男性</label>
      </span>
      <span>
        <input type="radio" id="woman" name="sex" value="woman" v-model="sex">
        <label for="woman">女性</label>
      </span>
      <button @click="calculationScore()">計算</button>
    </fieldset>

    <fieldset @click="calculationScore()">
      <p>
        <span>性格：</span>
        <span>
          <select name="personality" v-model="personalityScore">
            <option :value="`${scoresheet.personality.worst.score}`">{{scoresheet.personality.worst.name}}</option>
            <option :value="`${scoresheet.personality.bad.score}`">{{scoresheet.personality.bad.name}}</option>
            <option :value="`${scoresheet.personality.normal.score}`" selected>{{scoresheet.personality.normal.name}}</option>
            <option :value="`${scoresheet.personality.good.score}`">{{scoresheet.personality.good.name}}</option>
          </select>　
        </span>
        <span>{{personalityScore}}点</span>
      </p>
      <p>
        <span>経済力：</span>
        <span>
          <select name="economics" v-model="economicsScore">
            <option :value="`${scoresheet.economics.e0.score}`">{{scoresheet.economics.e0.name}}</option>
            <option :value="`${scoresheet.economics.e100.score}`">{{scoresheet.economics.e100.name}}</option>
            <option :value="`${scoresheet.economics.e200.score}`">{{scoresheet.economics.e200.name}}</option>
            <option :value="`${scoresheet.economics.e300.score}`">{{scoresheet.economics.e300.name}}</option>
            <option :value="`${scoresheet.economics.e400.score}`">{{scoresheet.economics.e400.name}}</option>
            <option :value="`${scoresheet.economics.e500.score}`">{{scoresheet.economics.e500.name}}</option>
            <option :value="`${scoresheet.economics.e600.score}`">{{scoresheet.economics.e600.name}}</option>
            <option :value="`${scoresheet.economics.e700.score}`">{{scoresheet.economics.e700.name}}</option>
            <option :value="`${scoresheet.economics.e800.score}`">{{scoresheet.economics.e800.name}}</option>
            <option :value="`${scoresheet.economics.e900.score}`">{{scoresheet.economics.e900.name}}</option>
            <option :value="`${scoresheet.economics.e1000.score}`">{{scoresheet.economics.e1000.name}}</option>
          </select>　
        </span>
        <span>{{economicsScore}}点</span>
      </p>
      <p>
        <span>健康（体型）：</span>
        <span>
          <select name="health" v-model="healthScore">
            <option :value="`${scoresheet.health.worst.score}`">{{scoresheet.health.worst.name}}</option>
            <option :value="`${scoresheet.health.bad.score}`">{{scoresheet.health.bad.name}}</option>
            <option :value="`${scoresheet.health.good.score}`">{{scoresheet.health.good.name}}</option>
          </select>　
        </span>
        <span>{{healthScore}}点</span>
      </p>
      <p>
        <span>親の同意：</span>
        <span>
          <select name="family_consensus" v-model="familyConsensusScore">
            <option :value="`${scoresheet.family_consensus.worst.score}`">{{scoresheet.family_consensus.worst.name}}</option>
            <option :value="`${scoresheet.family_consensus.bad.score}`">{{scoresheet.family_consensus.bad.name}}</option>
            <option :value="`${scoresheet.family_consensus.good.score}`">{{scoresheet.family_consensus.good.name}}</option>
          </select>　
        </span>
        <span>{{familyConsensusScore}}点</span>
      </p>
      <p>
        <span>容姿：</span>
        <span>
          <select name="looks" v-model="looksScore">
            <option :value="`${scoresheet.looks.l0.score}`">{{scoresheet.looks.l0.name}}</option>
            <option :value="`${scoresheet.looks.l10.score}`">{{scoresheet.looks.l10.name}}</option>
            <option :value="`${scoresheet.looks.l20.score}`">{{scoresheet.looks.l20.name}}</option>
            <option :value="`${scoresheet.looks.l30.score}`">{{scoresheet.looks.l30.name}}</option>
            <option :value="`${scoresheet.looks.l40.score}`">{{scoresheet.looks.l40.name}}</option>
            <option :value="`${scoresheet.looks.l50.score}`">{{scoresheet.looks.l50.name}}</option>
            <option :value="`${scoresheet.looks.l60.score}`">{{scoresheet.looks.l60.name}}</option>
            <option :value="`${scoresheet.looks.l70.score}`">{{scoresheet.looks.l70.name}}</option>
            <option :value="`${scoresheet.looks.l80.score}`">{{scoresheet.looks.l80.name}}</option>
            <option :value="`${scoresheet.looks.l90.score}`">{{scoresheet.looks.l90.name}}</option>
            <option :value="`${scoresheet.looks.god.score}`">{{scoresheet.looks.god.name}}</option>
          </select>　
        </span>
        <span>{{looksScore}}点</span> 
      </p>
      <p>
        <span>仕事への理解：</span>
        <span>
          <select name="work_understanding" v-model="workUnderstandingScore">
            <option :value="`${scoresheet.work_understanding.worst.score}`">{{scoresheet.work_understanding.worst.name}}</option>
            <option :value="`${scoresheet.work_understanding.bad.score}`">{{scoresheet.work_understanding.bad.name}}</option>
            <option :value="`${scoresheet.work_understanding.good.score}`">{{scoresheet.work_understanding.good.name}}</option>
          </select>　
        </span>
        <span>{{workUnderstandingScore}}点</span>  
      </p>
      <p>
        <span>年齢：</span>
        <span>
          <select name="age" v-model="ageScore">
            <option :value="`${scoresheet.age.u25.score}`">{{scoresheet.age.u25.name}}</option>
            <option :value="`${scoresheet.age.u30.score}`">{{scoresheet.age.u30.name}}</option>
            <option :value="`${scoresheet.age.u35.score}`">{{scoresheet.age.u35.name}}</option>
            <option :value="`${scoresheet.age.u40.score}`">{{scoresheet.age.u40.name}}</option>
            <option :value="`${scoresheet.age.u45.score}`">{{scoresheet.age.u45.name}}</option>
            <option :value="`${scoresheet.age.over45.score}`">{{scoresheet.age.over45.name}}</option>
          </select>　
        </span>
        <span>{{ageScore}}点</span>
      </p>
      <p>
        <span>職種：</span>
        <span>
          <select name="work" v-model="workScore">
            <option :value="`${scoresheet.work.bigcompany.score}`">{{scoresheet.work.bigcompany.name}}</option>
            <option :value="`${scoresheet.work.normalcompany.score}`">{{scoresheet.work.normalcompany.name}}</option>
            <option :value="`${scoresheet.work.bluecolor.score}`">{{scoresheet.work.bluecolor.name}}</option>
            <option :value="`${scoresheet.work.parttime.score}`">{{scoresheet.work.parttime.name}}</option>
            <option :value="`${scoresheet.work.nonwork.score}`">{{scoresheet.work.nonwork.name}}</option>
          </select>　
        </span>
        <span>{{workScore}}点</span>
      </p>
      <p>
        <span>家事能力：</span>
        <span>
          <select name="housework" v-model="houseworkScore">
            <option :value="`${scoresheet.housework.perfect.score}`">{{scoresheet.housework.perfect.name}}</option>
            <option :value="`${scoresheet.housework.good.score}`">{{scoresheet.housework.good.name}}</option>
            <option :value="`${scoresheet.housework.normal.score}`">{{scoresheet.housework.normal.name}}</option>
            <option :value="`${scoresheet.housework.bad.score}`">{{scoresheet.housework.bad.name}}</option>
            <option :value="`${scoresheet.housework.worst.score}`">{{scoresheet.housework.worst.name}}</option>
          </select>　
        </span>
        <span>{{houseworkScore}}点</span>
      </p>
      <p>
        <span>学歴：</span>
        <span>
          <select name="academy" v-model="academyScore">
            <option :value="`${scoresheet.academy.a100.score}`">{{scoresheet.academy.a100.name}}</option>
            <option :value="`${scoresheet.academy.a90.score}`">{{scoresheet.academy.a90.name}}</option>
            <option :value="`${scoresheet.academy.a80.score}`">{{scoresheet.academy.a80.name}}</option>
            <option :value="`${scoresheet.academy.a70.score}`">{{scoresheet.academy.a70.name}}</option>
            <option :value="`${scoresheet.academy.a60.score}`">{{scoresheet.academy.a60.name}}</option>
            <option :value="`${scoresheet.academy.a50.score}`">{{scoresheet.academy.a50.name}}</option>
            <option :value="`${scoresheet.academy.a40.score}`">{{scoresheet.academy.a40.name}}</option>          
            <option :value="`${scoresheet.academy.a30.score}`">{{scoresheet.academy.a30.name}}</option>          
            <option :value="`${scoresheet.academy.a20.score}`">{{scoresheet.academy.a20.name}}</option>          
            <option :value="`${scoresheet.academy.a10.score}`">{{scoresheet.academy.a10.name}}</option>            
            <option :value="`${scoresheet.academy.a0.score}`">{{scoresheet.academy.a0.name}}</option>
          </select>　
        </span>
        <span>{{academyScore}}点</span>
      </p>
    </fieldset>
    <p>婚活戦闘力：{{marriageScore.toFixed()}}点</p>
  </div>
</template>


<script>
import { defineComponent, ref } from 'vue'
import scoresheet from '../utilities/scoresheet.json'
import manspec from '../utilities/wanted_man_main_spec.json'
import womanspec from '../utilities/wanted_woman_main_spec.json'

export default defineComponent({
  name: "SpecInputForm",
  setup() {
    // 診断者情報
    const nickname = ref("名無しの権兵衛")
    const sex = ref("man")
    // 各要素得点
    const personalityScore = ref(66)
    const economicsScore = ref(50)
    const healthScore = ref(100)
    const familyConsensusScore = ref(50)
    const looksScore = ref(40)
    const workUnderstandingScore = ref(50)
    const ageScore = ref(40)
    const workScore = ref(50)
    const houseworkScore = ref(50)
    const academyScore = ref(40)
    // 婚活戦闘力
    const marriageScore = ref(0)
    // 戦闘力計算
    const spectotal = ref(0)
    const specsum = ref(0)
    const calculationScore = () => {
      let spec = {}
      if (sex.value === "man") {
        spec = manspec
      } else if (sex.value === "woman") {
        spec = womanspec
      }
      // 満点計算
      spectotal.value = 0
      for (let s in spec) {
        spectotal.value += spec[s]
      }
      // 加重平均計算
      specsum.value = 0
      specsum.value += spec.personality * personalityScore.value
      specsum.value += spec.economics * economicsScore.value
      specsum.value += spec.health * healthScore.value
      specsum.value += spec.family_consensus * familyConsensusScore.value
      specsum.value += spec.looks * looksScore.value
      specsum.value += spec.work_understanding * workUnderstandingScore.value
      specsum.value += spec.age * ageScore.value
      specsum.value += spec.work * workScore.value
      specsum.value += spec.housework * houseworkScore.value
      specsum.value += spec.academy * academyScore.value
      // 婚活戦闘力点数計算
      marriageScore.value = (specsum.value / spectotal.value)
      // 例外規定
      if (healthScore.value == 0 | looksScore.value == 0 | academyScore.value == 0) {
        marriageScore.value = 0
      }
    }
    calculationScore()
  

    return {
      nickname,
      sex,
      personalityScore,
      economicsScore,
      healthScore,
      familyConsensusScore,
      looksScore,
      workUnderstandingScore,
      ageScore,
      workScore,
      houseworkScore,
      academyScore,

      calculationScore,

      marriageScore,
      scoresheet
    };
  },
})

</script>


<style scoped>
.read-the-docs {
  color: #888;
}
</style>
