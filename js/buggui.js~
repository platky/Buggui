'use strict';

// This should be your main point of entry for your app
var canvas;
var ctx;
var clickedObj;
window.addEventListener('load', function() {
    var sceneGraphModule = createSceneGraphModule();
    var appContainer = document.getElementById('app-container');
    canvas = document.createElement('canvas');
    canvas.id= 'mainCanvas';
    canvas.height=600;
    canvas.width=800;
    appContainer.appendChild(canvas);
    ctx=canvas.getContext('2d');
    
    //temporary initial drawing
    var graph = new sceneGraphModule.GraphNode();
    var car = new sceneGraphModule.CarNode();
    var tire1 = new sceneGraphModule.TireNode('FRONT_RIGHT_TIRE_PART');
    var tire2 = new sceneGraphModule.TireNode('FRONT_LEFT_TIRE_PART');
    var tire3 = new sceneGraphModule.TireNode('BACK_RIGHT_TIRE_PART');
    var tire4 = new sceneGraphModule.TireNode('BACK_LEFT_TIRE_PART');
    var axle1 = new sceneGraphModule.AxleNode('FRONT_AXLE_PART');
    var axle2 = new sceneGraphModule.AxleNode('BACK_AXLE_PART');
    var trans = new AffineTransform();
    car.addChild(axle1);
    car.addChild(axle2);
    axle1.addChild(tire1);
    axle1.addChild(tire2);
    axle2.addChild(tire3);
    axle2.addChild(tire4);
    console.log(trans.toString());
    graph.initGraphNode(trans, graph.SCENE);
    graph.addChild(car);
    ctx.save();
    graph.render(ctx);
    ctx.restore();
    
    var final = new AffineTransform();
    var nTrans = new AffineTransform();
    var nRotate = new AffineTransform();
    var x;
    var y;
    
    canvas.addEventListener('mousedown', function() {
        console.log('canvas clicked');
        x =event.x-10;
        y = event.y-100;
        var nPoint = {x: x, y: y};
        console.log("x= "+nPoint.x+' and y=' +nPoint.y);
        var inThere =graph.pointInObject(nPoint);
    });
    
    canvas.addEventListener('mousemove', function() {
        if(clickedObj== "CAR_PART"){
            x =event.x-10-400;
            y = event.y-100-300;
            nTrans = new AffineTransform();
            final= new AffineTransform();
            nTrans.translate(x,y);
            final.concatenate(nRotate);
            final.concatenate(nTrans);
            car.updateTransform(final);
            canvas.width=canvas.width;
            ctx.save();
            graph.render(ctx);
            ctx.restore();
            appContainer.className= "move-cursor";
        } else if(clickedObj=="L_CAR_PART") {
            console.log("left");
            var x2 =event.x-10;
            var y2 = event.y-100;
            //console.log("x is "+x+" x2 is "+x2);
            if(x-x2 >0) {
                car.changeXScale(1);
            }else if (x-x2 <0) {
                car.changeXScale(-1);
            }
            x=x2;
            canvas.width=canvas.width;
            ctx.save();
            graph.render(ctx);
            ctx.restore();
            appContainer.className= "ew-cursor";
        } else if(clickedObj=="R_CAR_PART"){
            //console.log("right");
            var x2 =event.x-10;
            var y2 = event.y-100;
            //console.log("x is "+x+" x2 is "+x2);
            if(x2-x >0) {
                car.changeXScale(1);
            }else if (x2-x <0) {
                car.changeXScale(-1);
            }
            x=x2;
            canvas.width=canvas.width;
            ctx.save();
            graph.render(ctx);
            ctx.restore();
            appContainer.className= "ew-cursor";
        } else if(clickedObj=="T_CAR_PART") {
            //console.log("right");
            var x2 =event.x-10;
            var y2 = event.y-100;
            //console.log("x is "+x+" x2 is "+x2);
            if(y-y2 >0) {
                car.changeYScale(1);
            }else if (y-y2 <0) {
                car.changeYScale(-1);
            }
            y=y2;
            canvas.width=canvas.width;
            ctx.save();
            graph.render(ctx);
            ctx.restore();
            appContainer.className= "ns-cursor";
        } else if(clickedObj=="B_CAR_PART") {
            //console.log("right");
            var x2 =event.x-10;
            var y2 = event.y-100;
            //console.log("x is "+x+" x2 is "+x2);
            if(y2-y >0) {
                car.changeYScale(1);
            }else if (y2-y <0) {
                car.changeYScale(-1);
            }
            y=y2;
            canvas.width=canvas.width;
            ctx.save();
            graph.render(ctx);
            ctx.restore();
            appContainer.className= "ns-cursor";
        } else if(clickedObj=="TL_CAR_PART") {
            var x2 =event.x-10;
            var y2 = event.y-100;
            if(x-x2 >0) {
                car.changeXScale(1);
            }else if (x-x2 <0) {
                car.changeXScale(-1);
            }
            x=x2;
            if(y-y2 >0) {
                car.changeYScale(1);
            }else if (y-y2 <0) {
                car.changeYScale(-1);
            }
            y=y2;
            canvas.width=canvas.width;
            ctx.save();
            graph.render(ctx);
            ctx.restore();
            appContainer.className= "nw-cursor";
        } else if(clickedObj=="TR_CAR_PART") {
            var x2 =event.x-10;
            var y2 = event.y-100;
            if(x2-x >0) {
                car.changeXScale(1);
            }else if (x2-x <0) {
                car.changeXScale(-1);
            }
            x=x2;
            if(y-y2 >0) {
                car.changeYScale(1);
            }else if (y-y2 <0) {
                car.changeYScale(-1);
            }
            y=y2;
            canvas.width=canvas.width;
            ctx.save();
            graph.render(ctx);
            ctx.restore();
            appContainer.className= "ne-cursor";
        } else if(clickedObj=="BL_CAR_PART") {
            var x2 =event.x-10;
            var y2 = event.y-100;
            if(x-x2 >0) {
                car.changeXScale(1);
            }else if (x-x2 <0) {
                car.changeXScale(-1);
            }
            x=x2;
            if(y2-y >0) {
                car.changeYScale(1);
            }else if (y2-y <0) {
                car.changeYScale(-1);
            }
            y=y2;
            canvas.width=canvas.width;
            ctx.save();
            graph.render(ctx);
            ctx.restore();
            appContainer.className= "sw-cursor";
        } else if(clickedObj=="BR_CAR_PART") {
            var x2 =event.x-10;
            var y2 = event.y-100;
            if(x2-x >0) {
                car.changeXScale(1);
            }else if (x2-x <0) {
                car.changeXScale(-1);
            }
            x=x2;
            if(y2-y >0) {
                car.changeYScale(1);
            }else if (y2-y <0) {
                car.changeYScale(-1);
            }
            y=y2;
            canvas.width=canvas.width;
            ctx.save();
            graph.render(ctx);
            ctx.restore();
            appContainer.className= "se-cursor";
        }
        //rotating stuff
        else if (clickedObj=="T_ROTATE_PART"){
        console.log("rotate");
            var x2 =event.x-10;
            nRotate = new AffineTransform();
            var dif= x-x2;
                console.log("dif "+ dif);
            if(dif >0) {
                nRotate.rotate(-Math.PI*Math.abs(dif)/180, 0,0);
            }else if (dif <0) {
                nRotate.rotate(Math.PI*Math.abs(dif)/180, 0,0);
            }
            //x=x2;
            final= new AffineTransform();
            final.concatenate(nTrans);
            final.concatenate(nRotate);
            car.updateTransform(final);
            canvas.width=canvas.width;
            ctx.save();
            graph.render(ctx);
            ctx.restore();
            appContainer.className= "cell-cursor";
        } else if (clickedObj=="B_ROTATE_PART"){
            var x2 =event.x-10;
            nRotate = new AffineTransform();
            var dif= x-x2;
                console.log("dif "+ dif);
            if(dif >0) {
                nRotate.rotate(Math.PI*Math.abs(dif)/180, 0,0);
            }else if (dif <0) {
                nRotate.rotate(-Math.PI*Math.abs(dif)/180, 0,0);
            }
            //x=x2;
            final= new AffineTransform();
            final.concatenate(nTrans);
            final.concatenate(nRotate);
            car.updateTransform(final);
            canvas.width=canvas.width;
            ctx.save();
            graph.render(ctx);
            ctx.restore();
            appContainer.className= "cell-cursor";
        } else if(clickedObj=="FRONT_TIRE") {
            var x2 =event.x-10;
            var y2 = event.y-100;
            if(x2-x >0) {
                car.axleChange(-1);
            }else if (x2-x <0) {
                car.axleChange(1);
            }
            x=x2;
            //tire rotation
            if(y-y2 >0) {
                //car.changeYScale(1);
            }else if (y-y2 <0) {
                //car.changeYScale(-1);
            }
            y=y2;
            canvas.width=canvas.width;
            ctx.save();
            graph.render(ctx);
            ctx.restore();
        } else if(clickedObj=="BACK_TIRE") {
            var x2 =event.x-10;
            var y2 = event.y-100;
            if(x2-x >0) {
                car.axleChange(-1);
            }else if (x2-x <0) {
                car.axleChange(1);
            }
            x=x2;
            //tire rotation
            if(y-y2 >0) {
                //car.changeYScale(1);
            }else if (y-y2 <0) {
                //car.changeYScale(-1);
            }
            y=y2;
            canvas.width=canvas.width;
            ctx.save();
            graph.render(ctx);
            ctx.restore();
        }
    });
    
    canvas.addEventListener('mouseup', function() {
        clickedObj="";
        appContainer.className= "cursor";
    });
});

