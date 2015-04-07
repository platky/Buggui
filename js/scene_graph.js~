'use strict';

/**
 * A function that creates and returns the scene graph classes and constants.
 */
function createSceneGraphModule() {

    // Part names. Use these to name your different nodes
    var CAR_PART = 'CAR_PART';
    var FRONT_AXLE_PART = 'FRONT_AXLE_PART';
    var BACK_AXLE_PART = 'BACK_AXLE_PART';
    var FRONT_LEFT_TIRE_PART = 'FRONT_LEFT_TIRE_PART';
    var FRONT_RIGHT_TIRE_PART = 'FRONT_RIGHT_TIRE_PART';
    var BACK_LEFT_TIRE_PART = 'BACK_LEFT_TIRE_PART';
    var BACK_RIGHT_TIRE_PART = 'BACK_RIGHT_TIRE_PART';
    var SCENE = 'SCENE';
    var GraphNode = function() {
    };

    _.extend(GraphNode.prototype, {

        /**
         * Subclasses should call this function to initialize the object.
         *
         * @param startPositionTransform The transform that should be applied prior
         * to performing any rendering, so that the component can render in its own,
         * local, object-centric coordinate system.
         * @param nodeName The name of the node. Useful for debugging, but also used to uniquely identify each node
         */
        initGraphNode: function(startPositionTransform, nodeName) {

            this.nodeName = nodeName;

            // The transform that will position this object, relative
            // to its parent
            this.startPositionTransform = startPositionTransform;

            // Any additional transforms of this object after the previous transform
            // has been applied
            this.objectTransform = new AffineTransform();

            // Any child nodes of this node
            this.children = {};
            // Add any other properties you need, here
        },

        addChild: function(graphNode) {
            this.children[graphNode.nodeName] = graphNode;
        },

        /**
         * Swaps a graph node with a new graph node.
         * @param nodeName The name of the graph node
         * @param newNode The new graph node
         */
        replaceGraphNode: function(nodeName, newNode) {
            if (nodeName in this.children) {
                this.children[nodeName] = newNode;
            } else {
                _.each(
                    _.values(this.children),
                    function(child) {
                        child.replaceGraphNode(nodeName, newNode);
                    }
                );
            }
        },

        /**
         * Render this node using the graphics context provided.
         * Prior to doing any painting, the start_position_transform must be
         * applied, so the component can render itself in its local, object-centric
         * coordinate system. See the assignment specs for more details.
         *
         * This method should also call each child's render method.
         * @param context
         */
        render: function(context) {
            // TODO: Should be overridden by subclass
            //call CarNode
            //initial transform
            
            context.save();
            this.children[CAR_PART].render(context);//Draw The Car
            context.restore();
        },

        /**
         * Determines whether a point lies within this object. Be sure the point is
         * transformed correctly prior to performing the hit test.
         */
        pointInObject: function(point) {
            // TODO: There are ways to handle this query here, but you may find it easier to handle in subclasses
            //transform point
            var inThere =this.children[CAR_PART].pointInObject(point);
            return inThere;
        },
        
        updateTransform: function(transform){
            this.objectTransform = transform;
        }

    });

    var CarNode = function() {
        this.initGraphNode(new AffineTransform(), CAR_PART)
        //beginning area
        var x = 400;
        var y =300;
        this.startPositionTransform.translate(x,y);
        //for testing
        //this.startPositionTransform.rotate(Math.PI/6, 0,0);
        //this.startPositionTransform.scale(2,2);
        
        this.scaleX=0;
        this.scaleY=0;
    };

    _.extend(CarNode.prototype, GraphNode.prototype, {
        // Overrides parent method
        render: function(context) {
            context.save();
            context.transform(this.startPositionTransform.m00_, this.startPositionTransform.m10_, this.startPositionTransform.m01_,
            this.startPositionTransform.m11_,this.startPositionTransform.m02_,this.startPositionTransform.m12_);
            context.transform(this.objectTransform.m00_, this.objectTransform.m10_, this.objectTransform.m01_,
            this.objectTransform.m11_,this.objectTransform.m02_,this.objectTransform.m12_);
            this.children[FRONT_AXLE_PART].render(context);
            this.children[BACK_AXLE_PART].render(context);
            var sx = this.scaleX/2;
            var sy = this.scaleY/2;
            console.log("sx is " +sx);
            context.fillStyle="red";
            context.fillRect(-60-sx, -75-sy, 120+sx*2, 150+sy*2);
            context.strokeRect(-60-sx, -75-sy, 120+sx*2, 150+sy*2);
            context.save();
            context.translate(0,-65-sy);
            context.strokeRect(-60-sx,-10,120+sx*2,20);
            context.restore();
            context.save();
            context.translate(0,65+sy);
            context.strokeRect(-60-sx,-10,120+sx*2,20);
            context.restore();
            
            context.save();
            context.translate(0, -30-sy);
            context.fillStyle="blue";
            if(sy<=15 &&sy>=-20) {
                context.fillRect(-40-sx, -15-sy/2, 80+sx*2, 30+sy);
                context.strokeRect(-40-sx, -15-sy/2, 80+sx*2, 30+sy);
            } else if(sy<-20) {
                context.translate(0, -15);
                context.fillRect(-40-sx, -3, 80+sx*2, 6);
                context.strokeRect(-40-sx, -3, 80+sx*2, 6);
            } else if(sy>15) {
                context.fillRect(-40-sx, -22, 80+sx*2, 44);
                context.strokeRect(-40-sx, -22, 80+sx*2, 44);
            }
            context.restore();
            context.save();
            context.translate(0, 30+sy);
            context.fillStyle="blue";
            if(sy<=15 &&sy>=-20) {
                context.fillRect(-40-sx, -15-sy/2, 80+sx*2, 30+sy);
                context.strokeRect(-40-sx, -15-sy/2, 80+sx*2, 30+sy);
            } else if(sy<-20) {
                context.translate(0, 15);
                context.fillRect(-40-sx, -3, 80+sx*2, 6);
                context.strokeRect(-40-sx, -3, 80+sx*2, 6);
            } else if(sy>15) {
                context.fillRect(-40-sx, -22, 80+sx*2, 44);
                context.strokeRect(-40-sx, -22, 80+sx*2, 44);
            }
            context.restore();
            
            context.save();
            context.fillStyle = 'white';
            context.translate(-30-sx, -66-sy);
            context.fillRect(-8,-5, 16, 10);
            context.strokeRect(-8,-5, 16, 10);
            context.restore();
           
            context.save();
            context.fillStyle = 'white';
            context.translate(30+sx, -66-sy);
            context.fillRect(-8,-5, 16, 10);
            context.strokeRect(-8,-5, 16, 10);
            context.restore();
            
            
            context.restore();
        },

        // Overrides parent method
        pointInObject: function(point) {
            var inv = this.startPositionTransform.createInverse();
            var x = inv.m00_ * point.x + inv.m01_ *point.y + inv.m02_;
            var y = inv.m10_ * point.x + inv.m11_ * point.y + inv.m12_;
            var inv2 = this.objectTransform.createInverse();
            var x2 = inv2.m00_ * x + inv2.m01_ *y + inv2.m02_;
            var y2 = inv2.m10_ * x + inv2.m11_ * y + inv2.m12_;
            var nPoint = {x: x2, y: y2};
            //console.log('x at ' + nPoint.x + ' y at '+ nPoint.y);
            var sx = this.scaleX/2;
            var sy = this.scaleY/2;
            if(nPoint.x >=-60-sx && nPoint.x <=-50-sx) {
                if(nPoint.y>=-75-sy && nPoint.y<=-55-sy) {
                    clickedObj="TL_CAR_PART";
                } else if(nPoint.y >=55+sy && nPoint.y <=75+sy) {
                    clickedObj="BL_CAR_PART";
                } else if(nPoint.y>-55-sy && nPoint.y<55+sy){
                    clickedObj="L_CAR_PART";
                }
                return true;
            } else if(nPoint.x >=50+sx && nPoint.x <=60+sx) {
                if(nPoint.y>=-75-sy && nPoint.y<=-55-sy) {
                    clickedObj="TR_CAR_PART";
                } else if(nPoint.y >=55+sy && nPoint.y <=75+sy) {
                    clickedObj="BR_CAR_PART";
                } else if(nPoint.y>-55-sy && nPoint.y<55+sy) {
                    clickedObj="R_CAR_PART";
                }
                return true;
            } else if(nPoint.x >-50-sx && nPoint.x <50+sx) { //min size hit detection poor
                if(nPoint.y >=-75-sy && nPoint.y<=-55-sy) {
                    clickedObj="T_CAR_PART";
                } else if(nPoint.y >=55+sy && nPoint.y <=75+sy) {
                    clickedObj="B_CAR_PART";
                } else if(nPoint.y>=-45-sy && nPoint.y <=-15-sy) {
                    clickedObj="T_ROTATE_PART";
                } else if(nPoint.y>=15+sy && nPoint.y <=45+sy) {
                    clickedObj="B_ROTATE_PART";
                } else if(nPoint.y>-55-sy && nPoint.y<55+sy) {
                    clickedObj="CAR_PART";
                }
                return true;
            } else {
                var ret;
                ret=this.children[FRONT_AXLE_PART].pointInObject(nPoint);
                if(ret==true) {
                    return true;
                }
                ret=this.children[BACK_AXLE_PART].pointInObject(nPoint);
                return ret;
            }
            return false;
        },
        
        changeXScale: function(xval) {
            if(this.scaleX<=30 && this.scaleX >-95) {
                if(this.scaleX==30) {
                    if(xval<0) {
                        this.scaleX+=xval;
                    }
                }else if(this.scaleX==-95) {
                    if(xval>0){
                        this.scaleX+=xval;
                    }
                } else {
                    this.scaleX+=xval;
                }
            }
            this.children[FRONT_AXLE_PART].updateOff(this.scaleX);
            this.children[BACK_AXLE_PART].updateOff(this.scaleX);
        },
        
        changeYScale: function(yval) {
            if(this.scaleY<=50 && this.scaleY >-100) {
                if(this.scaleY==50) {
                    if(yval<0) {
                        this.scaleY+=yval;
                    }
                }else if(this.scaleY==-100) {
                    if(yval>0){
                        this.scaleY+=yval;
                    }
                } else {
                    this.scaleY+=yval;
                }
            }
            this.children[FRONT_AXLE_PART].updateTrans(this.scaleY);
            this.children[BACK_AXLE_PART].updateTrans(this.scaleY);
        },
        
        axleChange: function(val) {
            if(this.children[FRONT_AXLE_PART].extend<70 &&this.children[FRONT_AXLE_PART].extend>0) {
                this.children[FRONT_AXLE_PART].extend+=val;
                this.children[BACK_AXLE_PART].extend+=val;
            } else if(this.children[FRONT_AXLE_PART].extend==70) {
                if(val<0) {
                    this.children[FRONT_AXLE_PART].extend+=val;
                    this.children[BACK_AXLE_PART].extend+=val;
                }
            } else if(this.children[FRONT_AXLE_PART].extend==0) {
                if(val>0) {
                    this.children[FRONT_AXLE_PART].extend+=val;
                    this.children[BACK_AXLE_PART].extend+=val;
                }
            }
        }
    });

    /**
     * @param axlePartName Which axle this node represents
     * @constructor
     */
    var AxleNode = function(axlePartName) {
        this.initGraphNode(new AffineTransform(), axlePartName);
        this.offSet=0;
        this.extend=0;
        this.carSize=0;
        if(axlePartName == FRONT_AXLE_PART) {
            this.startPositionTransform.translate(0,-45);
        } else if(axlePartName == BACK_AXLE_PART) {
            this.startPositionTransform.translate(0,45);
        }
        
    };

    _.extend(AxleNode.prototype, GraphNode.prototype, {
        // Overrides parent method
        render: function(context) {
            context.save();
            context.transform(this.startPositionTransform.m00_, this.startPositionTransform.m10_, this.startPositionTransform.m01_,
            this.startPositionTransform.m11_,this.startPositionTransform.m02_,this.startPositionTransform.m12_);
            context.fillStyle="black";
            var x = this.carSize/2;
            if(this.nodeName == FRONT_AXLE_PART) {
                context.translate(0, -this.offSet/2);
            } else if(this.nodeName == BACK_AXLE_PART) {
                context.translate(0, this.offSet/2);
            }
            context.fillRect(-65-x-this.extend/2, -5, 130+x*2+this.extend, 10);
            
            if(this.nodeName == FRONT_AXLE_PART) {
                this.children[FRONT_RIGHT_TIRE_PART].render(context);
                this.children[FRONT_LEFT_TIRE_PART].render(context);
                this.children[FRONT_RIGHT_TIRE_PART].updateOff(this.extend);
                this.children[FRONT_LEFT_TIRE_PART].updateOff(this.extend);
            } else if(this.nodeName == BACK_AXLE_PART) {
                this.children[BACK_RIGHT_TIRE_PART].render(context);
                this.children[BACK_LEFT_TIRE_PART].render(context);
                this.children[BACK_RIGHT_TIRE_PART].updateOff(this.extend);
                this.children[BACK_LEFT_TIRE_PART].updateOff(this.extend);
            }
            context.restore();
        },

        // Overrides parent method
        pointInObject: function(point) {
            var inv = this.startPositionTransform.createInverse();
            var x = inv.m00_ * point.x + inv.m01_ *point.y + inv.m02_;
            var y = inv.m10_ * point.x + inv.m11_ * point.y + inv.m12_;
            var inv2 = this.objectTransform.createInverse();
            var x2 = inv2.m00_ * x + inv2.m01_ *y + inv2.m02_;
            var y2 = inv2.m10_ * x + inv2.m11_ * y + inv2.m12_;
            var nPoint = {x: x2, y: y2};
            var ret=false;
            if(this.nodeName == FRONT_AXLE_PART) {
                ret =this.children[FRONT_RIGHT_TIRE_PART].pointInObject(nPoint);
                ret =this.children[FRONT_LEFT_TIRE_PART].pointInObject(nPoint);
            } else if(this.nodeName == BACK_AXLE_PART) {
                ret =this.children[BACK_RIGHT_TIRE_PART].pointInObject(nPoint);
                ret =this.children[BACK_LEFT_TIRE_PART].pointInObject(nPoint);
            }
            return ret;
            //return false;
        },
        
        updateOff: function(val) {
            this.carSize = val;
            if(this.nodeName == FRONT_AXLE_PART) {
                this.children[FRONT_RIGHT_TIRE_PART].updateTrans(val);
                this.children[FRONT_LEFT_TIRE_PART].updateTrans(val);
            } else if(this.nodeName == BACK_AXLE_PART) {
                this.children[BACK_RIGHT_TIRE_PART].updateTrans(val);
                this.children[BACK_LEFT_TIRE_PART].updateTrans(val);
            }
        },
        
        updateTrans: function(val) {
            this.offSet=val;
        }
        
        
    });

    /**
     * @param tirePartName Which tire this node represents
     * @constructor
     */
    var TireNode = function(tirePartName) {
        this.initGraphNode(new AffineTransform(), tirePartName);
        this.out=0;
        this.offSet=0;
        if(tirePartName == FRONT_RIGHT_TIRE_PART) {
            this.startPositionTransform.translate(70,0);
        } else if(tirePartName == FRONT_LEFT_TIRE_PART) {
            this.startPositionTransform.translate(-70,0);
        } else if(tirePartName == BACK_LEFT_TIRE_PART) {
            this.startPositionTransform.translate(-70,0);
        }else if(tirePartName == BACK_RIGHT_TIRE_PART) {
            this.startPositionTransform.translate(70,0);
        }
    };

    _.extend(TireNode.prototype, GraphNode.prototype, {
        // Overrides parent method
        render: function(context) {
            context.save();
            context.transform(this.startPositionTransform.m00_, this.startPositionTransform.m10_, this.startPositionTransform.m01_,
            this.startPositionTransform.m11_,this.startPositionTransform.m02_,this.startPositionTransform.m12_);
            if(this.nodeName == FRONT_RIGHT_TIRE_PART || this.nodeName ==BACK_RIGHT_TIRE_PART) {//TODO fix to use other affine
                context.translate(this.out+this.offSet, 0);
                this.objectTransform = new AffineTransform();
                this.objectTransform.translate(this.out+this.offSet, 0);
            }else if(this.nodeName ==FRONT_LEFT_TIRE_PART || this.nodeName == BACK_LEFT_TIRE_PART) {
                context.translate(-this.out-this.offSet, 0);
                this.objectTransform = new AffineTransform();
                this.objectTransform.translate(-this.out-this.offSet, 0);
            }
            context.fillStyle="black";
            context.fillRect(-8, -25, 16, 50);
            context.strokeRect(-8, -25, 16, 50);
            context.restore();
        },

        // Overrides parent method
        pointInObject: function(point) {
            var inv = this.startPositionTransform.createInverse();
            var x = inv.m00_ * point.x + inv.m01_ *point.y + inv.m02_;
            var y = inv.m10_ * point.x + inv.m11_ * point.y + inv.m12_;
            var inv2 = this.objectTransform.createInverse();
            var x2 = inv2.m00_ * x + inv2.m01_ *y + inv2.m02_;
            var y2 = inv2.m10_ * x + inv2.m11_ * y + inv2.m12_;
            var nPoint = {x: x2, y: y2};
            if(nPoint.x >=-8 && nPoint.x <=8) {
                if(nPoint.y>=-25 && nPoint.y<=25) {
                    if(this.nodeName ==FRONT_RIGHT_TIRE_PART || this.nodeName ==FRONT_LEFT_TIRE_PART) {
                        clickedObj="FRONT_TIRE";
                    } else if(this.nodeName==BACK_RIGHT_TIRE_PART || this.nodeName ==BACK_LEFT_TIRE_PART) {
                        clickedObj="BACK_TIRE";
                    }
                    return true;
                }
            }
            return false;
        },
        
        updateTrans: function(val){
            this.out=val/2;
        },
        
        updateOff: function(val) {
            this.offSet=val/2;
        }
    });

    // Return an object containing all of our classes and constants
    return {
        GraphNode: GraphNode,
        CarNode: CarNode,
        AxleNode: AxleNode,
        TireNode: TireNode,
        CAR_PART: CAR_PART,
        FRONT_AXLE_PART: FRONT_AXLE_PART,
        BACK_AXLE_PART: BACK_AXLE_PART,
        FRONT_LEFT_TIRE_PART: FRONT_LEFT_TIRE_PART,
        FRONT_RIGHT_TIRE_PART: FRONT_RIGHT_TIRE_PART,
        BACK_LEFT_TIRE_PART: BACK_LEFT_TIRE_PART,
        BACK_RIGHT_TIRE_PART: BACK_RIGHT_TIRE_PART,
        SCENE: SCENE
    };
}


