<template>
    <canvas ref='canvas'></canvas>
</template>

<script>
//组件描述，父组件传入参数，组件使用数据操作dom。而不是响应式的驱动视图
//默认参数
//错误处理
import QRcode from 'qrcode'

export default {
    name: 'myqrcode',
    props: {
        infos: {
            type: Object,
            required: true
        }
    },
    watch: {
        infos(info){
            this.makeCode(info)
        }
    },
    methods: {
        /**
         * str： 二维码包含的信息
         * size: 二维码尺寸
         * margin: 二维码外边距
         * logo: 二维码logo
         * logoSize: 二维码尺寸
         * logoBgPadding: 二维码背景内边距
         * logoBgRadius: 二维码背景圆角弧度
         * logoBgColor: 二维码背景颜色
         */
        makeCode(params){
            //参数处理
            var str = params.str
            var size = params.size
            var margin = params.margin
            var logo = params.logo
            var logoSize = params.logoSize
            var logoBgPadding = params.logoBgPadding
            var logoBgRadius = params.logoBgRadius
            var logoBgColor = params.logoBgColor
            //画布准备
            var canvas = this.$refs.canvas
            var ctx = canvas.getContext('2d')
            var degree = Math.PI/180
            //绘制二维码
            var options = {
                errorCorrectionLevel: 'H',
                margin: margin,
                width: size
            }
            QRcode.toCanvas(canvas, str, options)
            //绘制logo背景
            // 右0(360) 下90 左180 上270
            var logoMargin = (size - logoSize)/2
            var lt = logoMargin - logoBgPadding
            var rb = logoMargin + logoSize + logoBgPadding
            //上线
            var topLineBeginX = lt + logoBgRadius
            var topLineBeginY = lt
            var topLineEndX = rb - logoBgRadius
            var topLineEndY = lt 
            ctx.moveTo(topLineBeginX, topLineBeginY)
            ctx.lineTo(topLineEndX, topLineEndY)
            //右线
            var rightLineBeginX = rb
            var rightLineBeginY = lt + logoBgRadius
            var rightLineEndX = rb 
            var rightLineEndY = lt 
            ctx.moveTo(rightLineBeginX,rightLineBeginY)
            ctx.lineTo(rightLineEndX,rightLineEndY)
            //下线
            var bottomLineBeginX = rb - logoBgRadius 
            var bottomLineBeginY = rb 
            var bottomLineEndX = lt + logoBgRadius 
            var bottomLineEndY = rb 
            ctx.moveTo(bottomLineBeginX, bottomLineBeginY)
            ctx.lineTo(bottomLineEndX, bottomLineEndY)
            //左线
            var leftLineBeginX = lt
            var leftLineBeginY = lt + logoBgRadius 
            var leftLineEndX = lt 
            var leftLineEndY = rb - logoBgRadius 
            ctx.moveTo(leftLineBeginX, leftLineBeginY)
            ctx.lineTo(leftLineEndX, leftLineEndY)
            //左上圆弧
            var leftTopX = lt + logoBgRadius 
            var leftTopY = lt + logoBgRadius 
            ctx.arc(leftTopX, leftTopY, logoBgRadius, degree*180, degree*270)
            //右上圆弧
            var rightTopX = rb - logoBgRadius
            var rightTopY = lt + logoBgRadius
            ctx.arc(rightTopX,rightTopY,logoBgRadius, degree*270, degree*360)
            //右下圆弧
            var rightBottomX = rb - logoBgRadius
            var rightBottomY = rb - logoBgRadius
            ctx.arc(rightBottomX, rightBottomY, logoBgRadius, 0, degree*90)
            //左下圆弧
            var leftBottomX = lt + logoBgRadius
            var leftBottomY = rb - logoBgRadius
            ctx.arc(leftBottomX, leftBottomY, logoBgRadius, degree*90,degree*180)
            ctx.closePath()
            ctx.fillStyle = '#ffffff'
            ctx.fill();
            //中间添加logo
            var logoImg = new Image()
            logoImg.src = logo
            logoImg.onload = function(){
                ctx.drawImage(logoImg, logoMargin, logoMargin, logoSize, logoSize)
            }
        }
    }
}
</script>

<style lang='less' scoped>
</style>