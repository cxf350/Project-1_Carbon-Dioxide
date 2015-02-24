# Project-1_Carbon-Dioxide

// Declaring and assigning values to the variables
int X_AXIS;
color c1= color(163, 210, 227);
color c2= color(145, 232, 146);
float x;
float y;
float carbon_dioxide = 0;
color c3, c4;

import controlP5.*;
ControlP5 cp5;

// Basic graphic setup
void setup() {

  size(600, 600);
  smooth();
  // Background gradient
  setGradient(0, 0, width, height, c2, c1, X_AXIS);

  frameRate(8);


  //smooth(); how is this important?


  cp5 = new ControlP5(this);
  cp5.addSlider("carbon_dioxide")
    .setRange(0, 5000)
      .setPosition(20, 20)
        .setSize(500, 10)
          .setNumberOfTickMarks(25);
}

void draw() {

  // Background gradient
  setGradient(0, 0, width, height, c2, c1, X_AXIS);


  //Drawing the small white circles

  float numEllipses = random(50, 100);

  for (int i =0; i < numEllipses; i++) {
    float x = random (width);
    float y = random (height);
    noStroke();
    fill(map(carbon_dioxide, 0, 5000, 255, 0), random(60, 255));
    ellipse (x, y, 6, 6);
  } 
  //Drawing the small red circles

  //float numEllipsesRed = random(5,25);
  float numEllipsesRed = (map(carbon_dioxide, 0, 5000, 0, 50));

  for (int i =0; i < numEllipsesRed; i++) {
    float x = random (width);
    float y = random (height);
    noStroke();
    fill(map(carbon_dioxide, 1000, 5000, 255, 255), 0, 0, random(10, 200));
    ellipse (x, y, 6, 6);
  }

  calcWave(carbon_dioxide);
  renderWave();
  float c3_ = map (carbon_dioxide, 0, 5000, 50, 255);
  c4 = color (c3_, 0, 255-c3_);
  c3 = color (0, 255-c3_, c3_);
}

//https://processing.org/examples/lineargradient.html
void setGradient(int x, int y, float w, float h, color c1, color c2, int axis ) {
  noFill();
  for (int i = x; i <= x+w; i++) {
    float inter = map(i, x, x+w, 0, 1);
    color c = lerpColor(c4, c3, inter);
    //color c = lerpColor(c1, c2, inter);
    stroke(c);
    line(i, y, i, y+h);
  }
}


