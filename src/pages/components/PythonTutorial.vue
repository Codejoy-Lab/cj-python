<template>
  <div class="tutorial-wrap">

    <div :class="dark? 'tutorial-content-wrap inner-dark':'tutorial-content-wrap'">

      <div :class='dark? stepWrap+" step-bar-dark" : stepWrap'>
        <div>
          <img :src="dark? forderDark:forderSrc" class="folder-img"/>
        </div>
        <div class="step-bars-wrap">
          <div class="radio-wrap" v-for="(item,index) in tutorials" :key="index">
            <input
              v-model="checkedValue"
              type="radio"
              :value="index"
              :id= "'radio' + index"
            />
            <label :v-for = "'radio' + index"></label>
          </div>
        </div>
      </div>
      <div :class="folded? 'folded':'tutorial'">
        <div class="tutorial-title">
          <span v-for="(item,index) in tutorials" :key="index" v-if="index=== checkedValue">{{item.step}}</span>
        </div>
        <div class="tutorial-content">
          <span v-for="(item,index) in tutorials" :key="index" v-if="index=== checkedValue">{{item.tutorial}}</span>
        </div>
      </div>
    </div>

  </div>
</template>

<script>
import stepLight from '../../assets/img/Step.png'
import stepDarl from '../../assets/img/step-dark.png'
import forder from '../../assets/img/folder.png'
import forderDark from '../../assets/img/folder-dark.png'

export default {
  name: 'PythonTutorial',
  props: {
    folded: Boolean,
    dark: Boolean
  },
  data () {
    return {
      checkedValue: 0,
      forderDark: forderDark,
      stepLight: stepLight,
      stepDark: stepDarl,
      forderSrc: forder,
      stepWrap: 'step-wrap',
      tutorialStyle: 'visibility: visible;',
      tutorials: [
        {id: '1', step: 'step1', tutorial: 'one', code: 'print("1step")'},
        {id: '2', step: 'step2', tutorial: 'two', code: 'print("2steps")'},
        {id: '3', step: 'step3', tutorial: 'three', code: 'print("3steps")'},
        {id: '4', step: 'step4', tutorial: 'four', code: 'print("4steps")'},
        {id: '5', step: 'step5', tutorial: 'five', code: 'print("4steps")'}
      ]
    }
  },
  methods () {

  }
}

</script>

<style lang="scss">
  @import '../../assets/style/index.scss';

  .tutorial-wrap {
    height: 100%;
    width: 100%;
    overflow: hidden;
  }

  .step-wrap {
    /* padding: 10px; */
    background: #c7e9f7;
    height: inherit;
    width: rem(50);
    height: 100%;
    text-align: center;
  }

  .step-bars-wrap {
    height: 100%;
    .radio-wrap {
      position:relative;
      display:flex;
      flex-direction: column;
      height:rem(50);
      &:after {
        content: "";
        height: rem(34);
        border: 1px solid #fff;
        position: absolute;
        top: rem(50);
        left: 50%;
        margin-top: rem(-18);
        transform: translateX(-50%);
        /*display:none;*/
      }
      input[type="radio"] {
        width: rem(14);
        height: rem(14);
        opacity: 1;
        z-index:11;
        position: absolute;
        left: 50%;
        top: 50%;
        transform:translate(-50%,-50%);
        margin:0;
        opacity:0;
        cursor: pointer;
      }

      label {
        position: absolute;
        left: 50%;
        top: 50%;
        width: rem(11);
        height: rem(11);
        border-radius: 50%;
        border: 1px solid #fff;
        transform:translate(-50%,-50%);
        z-index:10;
      }
      input:checked+label {
        background-color: #81D3FB;
        border: 1px solid #fff;
      }

      &:last-child {
        &:after {
          content: none;
        }
      }
      & .step-bars {
        margin: rem(15) 0;
        border-radius:50%;
        &:after {
          display: none;
        }
        &__label {
          padding: 0;
        }
      }
    }
  }

  .tutorial {
    width: 100%;
    /* font-family: 'Museo Sans Rounded 100'; */
    font-weight: 700;
    overflow: auto;
    &-title{
      display: block;
      width:100%;
      text-align:center;
    }
    &-content{

    }
  }

  .tutorial-content-wrap {
    width: 100%;
    display: flex;
    height: 100%;
  }

  .step-img {
    /* height: 60%; */
    width: 11px;
  }

  .folder-img {
    height: rem(26);
    margin: rem(16) 0 rem(24);
  }

  .folded {
    visibility: hidden;
    width: 0;
  }

  .step-bar-dark {
    background: #3c5267;
  }

  .inner-dark {
    background: #293C53;
    color: white;
  }
</style>
