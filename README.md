# Realidad-Aumentada


//Librerias OpenCV
import gab.opencv.*;
import processing.video.*;
import java.awt.*;

Capture video;
OpenCV opencv;

//Varibal de tipo PShape para almacenar en objeto.obj
PShape obj;
//Variable de tipo float para almacenar rotación de objeto 
float rotY;
float rotX;
//Inicilización de código
void setup() {
  //Tamaño del esenario con integracion 3D
  size(640, 480, P3D);
  //Inicilizacion de objeto video y OpenCV para inicilizar cámara
  video = new Capture(this, 640, 480);
  opencv = new OpenCV(this, 640, 480);
  opencv.loadCascade(OpenCV.CASCADE_FRONTALFACE);
  //Inicilización de la cámara  
  video.start();
  //Aisgnación a la variable obj la propiedad loadShape para leer la imágen
  //extensión .obj
  obj = loadShape("objeto.obj");
  //Escala del objeto importado (tamaño)
  obj.scale(15);
  //centrar pivot point del objeto 
  shapeMode(CENTER);
}

void draw() {
  
  opencv.loadImage(video);
  image(video, 0, 0);
  Rectangle[] faces = opencv.detect();
  println(faces.length);
  
  if (faces.length == 1) {
    translate(width/2, height/2);
    rotY = rotY + 5;
    rotX = rotX + 5;
    rotateY(radians(rotY));
    rotateX(radians(rotX));
  }
  shape(obj);
}

