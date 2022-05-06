# Teste2
Meu primeiro projeto JavaScript
let xBolinha = 300;
let yBolinha = 200;
let diametro = 15;
let raio = diametro / 2;

let velocidadeXBolinha = 10;
let velocidadeYBolinha = 10;

let colidiu = false;

//variáveis da raquete
let xRaquete = 5
let yRaquete = 150
let raqueteComprimento = 10
raqueteAltura = 90

//variáveis do oponente
let xRaqueteOponente = 585;
let yRaqueteOponente = 150;
let velocidadeYOponente;

//placar do jogo
let meusPontos = 0;
let pontosDoOponente = 0;

function setup() {
  createCanvas(600, 400);
}

function draw() {
  background(0,200,0);
  mostraBolinha();
  movimentaBolinha();
  verificaColisaoBorda();
  mostraRaquete(xRaquete, yRaquete);
  movimentaMinhaRaquete();
  //verificaColisaoRaquete();
  verificaColisaoRaquete(xRaquete, yRaquete);
  mostraRaquete(xRaqueteOponente, yRaqueteOponente);
  //movimentaRaqueteOponente();
  verificaColisaoRaquete(xRaqueteOponente, yRaqueteOponente);
  incluiPlacar();
  marcaPonto( );
  movimentaRaqueteOponente();
  circle(xBolinha,yBolinha,diametro);
  rect (xRaquete, yRaquete, raqueteComprimento, raqueteAltura);
  xBolinha += velocidadeXBolinha;
  yBolinha += velocidadeYBolinha;
  colidiu = collideRectRect(xRaquete, yRaquete, raqueteComprimento, raqueteAltura, xBolinha,yBolinha,raio);

  if (xBolinha + raio > width || xBolinha - raio < 0) {
    velocidadeXBolinha *= -1;
  }
  if (yBolinha + raio > height || yBolinha - raio < 0) {
    velocidadeYBolinha *= -1; 
}  
}
function movimentaBolinha() {
  xBolinha += velocidadeXBolinha;
  yBolinha += velocidadeYBolinha;
}

function mostraBolinha() {
  circle(xBolinha,yBolinha,diametro);
}
function verificaColisaoBorda() {
  if (xBolinha + raio > width || xBolinha - raio < 0) {
    velocidadeXBolinha *= -1;
  }
  if (yBolinha + raio > height || yBolinha - raio < 0) {
    velocidadeYBolinha *= -1; 
}  
}
function mostraRaquete() {
  rect (xRaquete, yRaquete, raqueteComprimento, raqueteAltura);
}
function movimentaMinhaRaquete() {
  if (keyIsDown(CONTROL)) {
    yRaquete += 10;
  }
  if (keyIsDown(SHIFT)) {
    yRaquete -= 10;
  }
}
function verificaColisaoRaquete() {
  if (xBolinha - raio < xRaquete + raqueteComprimento
     && yBolinha - raio < yRaquete + raqueteAltura
     && yBolinha + raio > yRaquete) {
    velocidadeXBolinha *= -1;
  }
}
function mostraRaqueteOponente() {
  rect (xRaqueteOponente, yRaqueteOponente, raqueteComprimento, raqueteAltura);
}
function mostraRaquete(x,y) {
  rect(x, y, raqueteComprimento, raqueteAltura);
}
function movimentaRaqueteOponente() {
  velocidadeYOponente = yBolinha - yRaqueteOponente - raqueteComprimento / 2 - 30;
  yRaqueteOponente += velocidadeYOponente
}
function colisaoMinhaRaqueteBiblioteca() {
  colidiu = collideRectRect(xRaquete, yRaquete, raqueteComprimento, raqueteAltura, xBolinha,yBolinha,raio);
  if (colidiu) {
    velocidadeXBolinha *= -1;
  }
}
function verificaColisaoRaquete(x, y) {
  colidiu = collideRectCircle(x, y, raqueteComprimento, raqueteAltura, xBolinha, yBolinha, raio);
  if (colidiu){
    velocidadeXBolinha *= -1;
  }
}
function incluiPlacar() {
  fill(255,50,100);
  text(meusPontos, 100, 26); 
  text(pontosDoOponente, 500, 26);
}
function marcaPonto( ){
  if (xBolinha > 590) {
    meusPontos += 1;
  }
  if (xBolinha < 10) {
    pontosDoOponente += 1;
  }
}
function movimentaRaqueteOponente() {
  if (keyIsDown(UP_ARROW)) {
    yRaqueteOponente -= 10;
  }
  if (keyIsDown(DOWN_ARROW)) {
    yRaqueteOponente += 10;
  }
}
