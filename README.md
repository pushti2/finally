# finally
var PLAY=1;
var END=0;
var gameState=1;

var sword,swordImage;
var fruit1,fruit2,fruit3,fruit4,fruit,fruitsGroup;
var alien, alienImage,aliensGroup;
var score;
var gameoverImage;

function preload(){
  swordImage=loadImage('sword.png');
  fruit1=loadImage('fruit1.png');
  fruit2=loadImage('fruit2.png');
  fruit3=loadImage('fruit3.png');
  fruit4=loadImage('fruit4.png');
  alienImage=loadAnimation(" alien1.png","alien2.png");
  gameoverImage =loadImage("gameover.png");
}

function setup(){
  createCanvas(600,600);
  
  sword=createSprite(200,300,20,10);
  sword.addImage("moving",swordImage);
  sword.scale=0.8;
  sword.setCollider("rectangle",0,0,40,40);

  
  fruitsGroup = createGroup();
  aliensGroup = createGroup();
  
    score=0 
 
}


function draw(){
  background("lightblue")
  if(gameState===PLAY){
    
    aliens();
    fruits();
    
     sword.y=World.mouseY;
     sword.x=World.mouseX;
  
   
  if( fruitsGroup.isTouching(sword)){
    fruitsGroup.destroyEach();
    score=score+1;
  }
 else{
   if(aliensGroup.isTouching(sword)){
        gameState=END;
        
        fruitsGroup.destroyEach();
        aliensGroup.destroyEach();
        fruitsGroup.setVelocityXEach(0);
        aliensGroup.setVelocityXEach(0);
        
        // Change the animation of sword to gameover and reset its position
        sword.addImage("moving",gameoverImage);
        sword.x=300;
        sword.y=200;
        sword.scale=1;
      }
    }
   }
  
drawSprites()
  text("Score: " + score, 500, 50);

}

function fruits(){
  if(World.frameCount%80===0){
   fruit=createSprite(600,200,20,20);
    fruit.scale=0.2;
    var r = Math.round(random(1,4));
    if(r == 1){
      fruit.addImage(fruit1);
    }else if(r == 2){
     fruit.addImage(fruit2);
    }else if(r == 3){
      fruit.addImage(fruit3);
    }else{
      fruit.addImage(fruit4);
    }
    fruit.y =Math.round(random(80,340));
    fruit.velocityX=-7;
    fruit.setLifetime=100;
    
    
    fruitsGroup.add(fruit);
  }
}  

function aliens(){
  if(World.frameCount%200===0){
    alien=createSprite(400,200,20,20);
 alien.addAnimation("monster",alienImage);
    alien.y =Math.round(random(60,340));
    alien.velocityX=-8;
    alien.setLifetime=50;
    
    aliensGroup.add(alien);
  }
}
