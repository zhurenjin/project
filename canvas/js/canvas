//canvas形成微信模板嵌套，华体微课内容公众号
var modellist = [
    //背景图片
    {
        src:'images/model1.jpg',
        x:0,
        y:0,
        w:750,
        h:1334,
        t:'img',
    },
    //微信头像
    {
        src:'images/timg.jpg',
        x:306,
        y:293,
        w:138,
        h:138,
        t:'circularimg',
    },
    //二维码链接
    {
        src:"https://www.baidu.com/",
        x:239,
        y:1067,
        w:110,
        h:110,
        t:'qrcode',
    },
    //中部图片
    {
        src:'images/timg.jpg',
        x:116,
        y:518,
        w:520,
        h:262,
        t:'img',
    },

];
var testlist = [
    {
        test:'快手省老铁市双击县没毛病镇666村 ',
        x:90,
        y:850,
        t:'test',
        font:'30px Arial',
        color:'#000',
    },
    {
        test:'尚德机构',
        x:336,
        y:260,
        t:'test',
        font:'22px Georgia',
        color:'#fff',
    },
    {
        test:'阿尼玛老铁666',
        x:320,
        y:464,
        t:'test',
        font:'20px Georgia',
        color:'blue',
    },
];
window.onload = function(){
    modellist.forEach((v,i)=>{
        if(v.t=="circularimg"){
            circularImg(v.src,function() {
                // $('#show').attr('src',this.src)
                v.base64src = this.src
            })
        }else if(v.t=="qrcode"){
            qrcodeBase64(v.src,function() {
                v.base64src = this.src
            })
        }else{
            v.base64src=v.src;
        }
    });
};

//裁剪出圆形,微信头像
var circularImg = function(img,fu){
    if (typeof img !== 'object') {
        var tem = new Image();
        tem.src = img;
        tem.onload=function(){
            img = tem;
            var w, h, _canv, _contex, cli;
            if (img.width > img.height) {
                w = img.height;
                h = img.height;
            } else {
                w = img.width;
                h = img.width;
            }
            _canv = document.createElement('canvas');
            _canv.width = w;
            _canv.height = h;
            _contex = _canv.getContext("2d");
            cli = {
                x: w / 2,
                y: h / 2,
                r: w / 2
            };
            _contex.clearRect(0, 0, w, h);
            _contex.save();
            _contex.beginPath();
            _contex.arc(cli.x, cli.y, cli.r, 0, Math.PI * 2, false);
            _contex.clip();
            _contex.drawImage(img, 0, 0);
            _contex.restore();

            var img1=new Image();
            img1.src=_canv.toDataURL();
            img1.onload =fu;
        }
    }
}

//返回二维码Base64
var qrcodeBase64 = function(test,fu){
    var $qrcode = $('#Model1');
    $qrcode.html('');
    var qrcode = new QRCode('Model1'+'', {
        text: test,
        width: 130,
        height: 130,
        context: "",
        //  correctLevel: QRCode.CorrectLevel.H
    });
    var img=qrcode._oDrawing._elImage;
    img.onload =fu;
}

var c=document.createElement('canvas');
var ctx=c.getContext('2d');//画布大小
c.width=750;
c.height=1334;
ctx.rect(0,0,c.width,c.height);
ctx.fillStyle='#fff';
ctx.fill();
var list=modellist;
function F1(i,list){
    var img=new Image();
    if(list[i].base64src){
        img.src=list[i].base64src;
        img.onload=function(){
            ctx.drawImage(img,list[i].x,list[i].y,list[i].w,list[i].h);
            if(list.length==i+1){
                for(var vi=0;vi< testlist.length;vi++){
                    var gradient=ctx.createLinearGradient(0,0,c.width,0);
                    gradient.addColorStop("0",testlist[vi].color);
                    gradient.addColorStop("0.5",testlist[vi].color);
                    gradient.addColorStop("1.0",testlist[vi].color);
                    ctx.fillStyle=gradient;
                    ctx.font=testlist[vi].font;
                    // ctx.fillText(testlist[vi].test,testlist[vi].x,testlist[vi].y);
                    //文字换行的显示
                    if(vi==0){
                        var lineWidth = 0;
                        var canvasWidth = c.width-180;//计算canvas的宽度
                        var initHeight=testlist[0].y;//绘制字体距离canvas顶部初始的高度
                        var lastSubStrIndex= 0; //每次开始截取的字符串的索引
                        for(let i=0;i<testlist[0].test.length;i++){
                            lineWidth+=ctx.measureText(testlist[0].test[i]).width;
                            if(lineWidth>canvasWidth){
                                ctx.fillText(testlist[0].test.substring(lastSubStrIndex,i),testlist[0].x,initHeight);
                                initHeight+=38;//38为字体的高度
                                lineWidth=0;
                                lastSubStrIndex=i;
                            }
                            if(i==testlist[0].test.length-1){//绘制剩余部分
                                ctx.fillText(testlist[0].test.substring(lastSubStrIndex,i+1),testlist[0].x,initHeight);
                            }
                        }
                    }else{
                        ctx.fillText(testlist[vi].test,testlist[vi].x,testlist[vi].y);
                    }
                }

                var base64=c.toDataURL('image/jpeg');
                var img1=document.getElementById('show');
                img1.setAttribute('src',base64);
            }else{
                F1(i+1,list);
            }
        }
    }else{
        setTimeout(function () {
            F1(i,list);
        }, 100);
    }
}
F1(0,list);
