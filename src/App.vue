<template>
    <div id="box">
        <canvas id="canvas"></canvas>
        <button id='drawAll'>一键加码</button>
        <button id='clearAll'>还原</button>
    </div>
</template>
<script>
    import Mosaic from 'image-mosaic'
    export default {
        name: "imageMosaic",

        data()
        {return {imgSrc:'https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fpic26.nipic.com%2F20130115%2F8952533_013300701165_2.jpg&refer=http%3A%2F%2Fpic26.nipic.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1625141261&t=58fa8a2e8eb2e0549a6fe10c481d3faa'}
        },
        mounted()
        {
            this.initMosaic()
        }
        ,
        methods: {
            drawImageToCanvas()
            {
                const canvas = document.getElementById('canvas')
                const ctx = canvas.getContext('2d')
                let imageUrl
                if (this.imgSrc) {
                    imageUrl = this.imgSrc
                }
                return new Promise((resolve) => {
                    const image = new Image()
                    image.crossOrigin = 'Annoymous'
                    image.onload = function () {
                        canvas.width = image.width
                        canvas.height = image.height
                        ctx.drawImage(this, 0, 0, image.width, image.height)
                        resolve(ctx)
                    }
                    image.src = imageUrl
                })
            }
            ,
            initMosaic()
            {
                this.drawImageToCanvas().then(ctx => {
                    const mosaic = new Mosaic(ctx)
                    const MouseEvents = {
                        init() {
                            mosaic.context.canvas.addEventListener('mousedown', MouseEvents.mousedown)
                        },
                        mousedown() {
                            mosaic.context.canvas.addEventListener('mousemove', MouseEvents.mousemove)
                            document.addEventListener('mouseup', MouseEvents.mouseup)
                        },
                        mousemove(e) {
                            if (e.shiftKey) {
                                mosaic.eraseTileByPoint(e.layerX, e.layerY)
                                return
                            }
                            mosaic.drawTileByPoint(e.layerX, e.layerY)
                        },
                        mouseup() {
                            mosaic.context.canvas.removeEventListener('mousemove', MouseEvents.mousemove)
                            document.removeEventListener('mouseup', MouseEvents.mouseup)
                        }
                    }
                    MouseEvents.init()
                    document.querySelector('#drawAll').addEventListener('click', () => {
                        mosaic.drawAllTiles()
                    })
                    document.querySelector('#clearAll').addEventListener('click', () => {
                        mosaic.eraseAllTiles()
                    })
                })
            }
        }
    };


</script>
<style scoped>

</style>