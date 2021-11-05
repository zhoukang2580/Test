<template>
    <div class="score">
        <div class="your_score_container">
            <div class="your_scores">{{score}}分!</div>
            <div class="result_tip">
                {{scoreTips}}
            </div>
        </div>
        <div class="share_button" @click="getScoreShow()"></div>
        <div class="share_code">
            <header class="share_header">关注葡萄之家，获取答案。</header>
            <img src="../../assets/4-4.png" height="212" width="212" class="code_img"> 
        </div>
        <div v-show="isShow" class="isScoreShow" @click="getScoreShow()">
            <img class="share_img" src="../../assets/5-2.png" alt="">
        </div>
    </div>
</template>

<script>
import { mapState } from 'vuex'
export default {
    name:'score',
    data(){
        return{
            score:0,
            isShow:false,
            scoreTips:'',
            rightAnswer: [2, 7, 12, 13, 18], //正确答案
            scoreTipsArr:['你说，是不是把知识都还给小学老师了？','还不错，但还需要继续加油哦！','不要嘚瑟还有进步的空间！','智商离爆表只差一步了！','你也太聪明啦，葡萄之家欢迎你！'],
        }
    },
    computed:mapState(['answerid']),
    methods:{
        computedScore(){
            this.answerid.forEach((e,ind) => {
                console.log(ind,e)
                if (e == this.rightAnswer[ind]) {
                    this.score += 20;
                }
            });
        },
        getScoreTips(){
            let index = Math.ceil(this.score/20)-1;
            console.log(index,'index');
            this.scoreTips = this.scoreTipsArr[index];
            console.log(this.scoreTips);
        },

        getScoreShow(){
            this.isShow = !this.isShow;
        }
    },
    created(){
        this.computedScore();
        this.getScoreTips();
        // document.body.style.backgroundImage = 'url(../../assets/4-1.jpg)'
    }
}
</script>

<style lang="less">
    body{
        background-image: url(../../assets/4-1.jpg);
        padding-top: 3.2rem;
    }

    .your_score_container{
        width: 14.7rem;
        height: 14.1rem;
        background: url(../../assets/4-2.png) no-repeat;
        background-size: 100% 100%;
        margin: auto;
        position: relative;
        .your_scores{
            font-size: 2rem;
            position: absolute;
            text-indent: 5.5rem;
            top: 6.8rem;
            font-weight: 900;
            -webkit-text-stroke: 0.05rem #412318;
            font-family: 'Microsoft YaHei';
            font-family: Tahoma,Helvetica,Arial;
            color: #a51d31;
        }

        .result_tip{
            position: absolute;
            top: 10rem;
            width: 14rem;
            left: 0.6rem;
            color: #3e2415;
            text-align: center;
        }
    }

    .share_button{
        background: url(../../assets/4-3.png) no-repeat;
        width: 6.025rem;
        height: 2.9rem;
        background-size: 6.4rem 100%;
        margin: 2.2rem auto 0;
    }

    .share_code{
        width: 8.3rem;
        margin: 1.5rem auto 0;
        .share_header{
            color: #664718;
            font-size: 0.475rem;
            font-family: 'Microsoft YaHei';
            width: 9rem;
            font-weight: 500;
        }
        .code_img{
            height: 8.3rem;
            width: 8.3rem;
            margin-top: 0.5rem;
        }
    }

    .isScoreShow{
        position: fixed;
        bottom: 0;
        right: 0;
        top: 0;
        left: 0;
        background: url(../../assets/5-1.png) no-repeat;
        background-size: 100% 100%;
        opacity: 0.92;
        .share_img{
            height: 10.975rem;
            width: 11.95rem;
            position: fixed;
            top: 0.5rem;
            left: 50%;
            margin-left: -5.975rem;
        }
    }
</style>

