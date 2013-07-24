tester-tester
=============
Maxim maxim;
AudioPlayer player_open_bell, player_close_bell, player_OM, player_rain, player_woods, player_zen;

//for timer
int passedTime;
int savedTime15;
int totalTime15 = 5000; //9000000;

int savedTime20;
int totalTime20 = 12000000;

int savedTime30;
int totalTime30 = 18000000;

//for sun
int num = 256;
float rot = TWO_PI/num;
float innerRadZero, outerRad = 200;//250
float barrier = 0.96;



boolean playing = false;



PImage tip, buddha, branch, menu, bowl1, bowl2, bowl3, lotus, om, cloud, meditation_menu;


void setup() 

{
  size(1024, 768);
  
  //How to load cover page 'menu'? click anywhere on it to be taken to main page?
  //PImage menu = loadImage("meditation_menu.png");
  //background(menu);

  savedTime15 = millis();
  savedTime20 = millis();
  savedTime30 = millis();

  tip = loadImage("Joshua.jpg");
  buddha = loadImage("buddha.png");
  lotus = loadImage("img05.png");
  branch = loadImage("img06.png");
  bowl1 = loadImage("bowl1.png");
  bowl2 = loadImage("bowl3.png");
  bowl3 = loadImage("bowl2.png");
  om = loadImage("om.png");
  cloud = loadImage("cloud.png");
  menu = loadImage("meditation_menu.png");

  imageMode(CENTER);


  maxim = new Maxim(this);
  //load new files for bowls

  player_open_bell = maxim.loadFile("start_bell.wav");
  player_open_bell.setLooping(false);

  player_close_bell = maxim.loadFile("end_bell.wav");
  player_close_bell.setLooping(false);

  player_OM = maxim.loadFile("OM.wav");//OM image
  player_OM.setLooping(true);

  player_rain = maxim.loadFile("rain3.wav"); //cloud image
  player_rain.setLooping(true);

  player_woods = maxim.loadFile("woods.wav"); //branch image
  player_woods.setLooping(true);

  player_zen = maxim.loadFile("zen_music.wav"); //lotus image
  player_zen.setLooping(false);


// end of setup
}

void draw() 

{  

    image(tip, width/2, height/2, width, height);
    fill(0);



//need this: if bowl1 mouseReleased, play player_start_bell && start timer, 

//when timer ends play player_close_bell 1x

//same for all bowls

//and for image buttons:

//if mouseReleased == branch image, player woods starts looping until clicked off or until end bell  tiggered 
//(if end bell then all other buttons off)

//Same set up for all buttons and sounds, can all be on at once, but for bowls can only be on one at a time

    // Calculate how much time has passed

    int passedTime = millis() - savedTime15;
        passedTime = millis() - savedTime20;
        passedTime = millis() - savedTime30;
   
   
      //menu,instruction buttons
      PImage uiImage = loadImage("bowl1.png");
      image (uiImage, 100, 100);

      uiImage = loadImage("bowl3.png");
      image (uiImage, 100, 200);

      uiImage = loadImage("bowl2.png");
      image (uiImage, 100, 300);

      uiImage = loadImage("img06.png");//branch
      image (uiImage, 950, 600);

      uiImage = loadImage("img05.png");//lotus
      image (uiImage, 950, 500);

      uiImage = loadImage("om.png");
      image (uiImage, 950, 700);

      uiImage = loadImage("cloud.png");
      image (uiImage, 950, 400);

      uiImage = loadImage("buddha.png");
      image (uiImage, 300, 650);
    


    //forsun
    {
      //background();
      stroke(255, 255, 105);
      //translate(width/5, height/5);
      translate(width/1, height/10);
      strokeWeight(0.8);//.5
      beginShape(LINES);
      for (int i=0; i<num; i++) 
      {
        float angle = i*rot;
        float x = cos(angle);
        float y = sin(angle);
        float innerRad = 75 + 10*sin( radians(360*noise(i*0.015)) + millis()*0.001);//.003
        if (i == 0) 
        {
          innerRadZero = innerRad;
        } 
        else if (i>num*barrier) 
        {
          float perc = map(i, num*barrier, num, 0, 1);
          innerRad = lerp(innerRad, innerRadZero, perc);
        }
        line(x*innerRad, y*innerRad, x*outerRad, y*outerRad);
      }
      endShape();
    
    }
}

//void mousePressed()


  void mouseReleased()
  {
    
    //bowl1
    //ISSUE - both bells set off when clicked, timer does not work.//now both start and end bell go at same time
    
    if(mouseX > 100 && mouseX < 130 && mouseY > 100 && mouseY < 120)
    
    {  
       player_open_bell = maxim.loadFile("start_bell.wav");
       player_open_bell.cue(0);
       player_open_bell.play();
       player_open_bell.setLooping(false);
    }
      
    
    
    if (mouseX > 100 && mouseX < 130 && mouseY > 100 && mouseY < 120 &&  passedTime > totalTime15 )
   
    {
     //player_close_bell.stop();
     player_close_bell.cue(0);
     player_close_bell.play();
     player_close_bell.setLooping(false);
      println( " 5 seconds have passed! " );
      //background(random(255)); // Color a new background
     savedTime15 = millis(); // Save the current time to restart the timer!
    }
    
    //bowl2
    
    
     if(mouseX > 100 && mouseX < 130 && mouseY > 300 && mouseY < 330)
    
    {  
       player_open_bell = maxim.loadFile("start_bell.wav");
       player_open_bell.cue(0);
       player_open_bell.play();
       player_open_bell.setLooping(false);
    }
    
    
      passedTime = millis() - savedTime20;
      if  (mouseX > 100 && mouseX < 130 && mouseY > 300 && mouseY < 330 &&  passedTime > totalTime20 )
      {
        
     //player_close_bell.stop();
     player_close_bell.cue(0);
     player_close_bell.play();
     player_close_bell.setLooping(false);
      println( " 20 minutes have passed! " );
      //background(random(255)); // Color a new background
     savedTime20 = millis(); // Save the current time to restart the timer!
    }
    
    
    
    //bowl3
     if(mouseX > 100 && mouseX < 130 && mouseY > 200 && mouseY < 220)
    
    {  
       player_open_bell = maxim.loadFile("start_bell.wav");
       player_open_bell.cue(0);
       player_open_bell.play();
       player_open_bell.setLooping(false);
    }
    
      passedTime = millis() - savedTime30;
      if  (mouseX > 100 && mouseX < 130 && mouseY > 200 && mouseY < 220 &&  passedTime > totalTime30 )
      {
        
     //player_close_bell.stop();
     player_close_bell.cue(0);
     player_close_bell.play();
     player_close_bell.setLooping(false);
      println( " 30 minutes have passed! " );
      //background(random(255)); // Color a new background
     savedTime30 = millis(); // Save the current time to restart the timer!
    }
    
   { 
    
    //cloud - rain works properly, clicks on and off. Other buttons work, but won't turn off, 
    //and OM button starts new loops resulting in overlapping audio.
    
    if(mouseX > 950 && mouseX < 980 && mouseY > 400 && mouseY < 420)
    
    {  
       player_rain = maxim.loadFile("rain3.wav"); 
       player_rain.cue(0);
       player_rain.play();
       player_rain.setLooping(true);
    }
    else 
    {
    player_rain.stop();
    playing = false;
  }
      
   }
    
    {
    //lotus
    if(mouseX > 950 && mouseX < 970 && mouseY > 500 && mouseY < 520)
    
    {  
       player_zen = maxim.loadFile("zen_music.wav");
       player_zen.cue(0);
       player_zen.play();
       player_zen.setLooping(true);
    }
    
    else 
    {
    player_zen.stop();
    playing = false;
  }
      
    }
    {
    //branch
    if(mouseX > 950 && mouseX < 970 && mouseY > 600 && mouseY < 630)
    
    {  
       player_woods = maxim.loadFile("woods.wav");
       player_woods.cue(0);
       player_woods.play();
       player_woods.setLooping(true);
    }
    
    else 
    {
    player_woods.stop();
    playing = false;
  }
      
    }
   { 
    //OM
    if(mouseX > 950 && mouseX < 970 && mouseY > 700 && mouseY < 730)
    
    {  
       player_OM = maxim.loadFile("OM.wav");
       player_OM.cue(0);
       player_OM.play();
       player_OM.setLooping(true);
    }
    
    else 
    {
    player_OM.stop();
    playing = false;
  }
      
  }
  }
  
      
    

