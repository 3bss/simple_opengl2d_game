#include <math.h>
#include <stdio.h>
#include <string.h>
#include <glut.h>

int p0[2];
int p1[2];
int p2[2];
int p3[2];
//int tar = 4;
int x = 0;
int y = 0;
int shark = 0;

static int WINDOW_WIDTH, WINDOW_HEIGHT;

int timer=0;
float t = 0;

int defX = 1;
float move1 = 5.5;
float move2 = 5.5;
bool firing = false;
bool throw1 = false;
bool throw2 = false;
bool b1 = true;
bool b2 = false;
int health1 = 40;
int health2 = 490;
int pp1 = 0;
int pp2 = 0;
char * z= "";


int right =0;
int right2 = 0;



bool ended = false;
//char* string = "ahahah";



bool defender_visible = true;
bool defender_hit = false;
static int playerturn = 0; //(0)player 1turn && (1) player2 turn
static int mouseclick = 0;



void print(int x, int y, char* string)
{
	int len, i;

	//set the position of the text in the window using the x and y coordinates
	glRasterPos2f(x, y);

	//get the length of the string to display
	len = (int)strlen(string);

	//loop to display character by character
	for (i = 0; i < len; i++)
	{
		glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_24, string[i]);
	}
}

int* bezier(float t, int* p0, int* p1, int* p2, int* p3)
{
	int res[2];
	res[0] = pow((1 - t), 3) * p0[0] + 3 * t * pow((1 - t), 2) * p1[0] + 3 * pow(t, 2) * (1 - t) * p2[0] + pow(t, 3) * p3[0];
	res[1] = pow((1 - t), 3) * p0[1] + 3 * t * pow((1 - t), 2) * p1[1] + 3 * pow(t, 2) * (1 - t) * p2[1] + pow(t, 3) * p3[1];
	return res;
}




struct Defender
{
	float left, top, right, bottom;
};
Defender d = { 0,200,100,170};

void DrawRectangle(Defender  def)
{
//glTranslated(defX, 0, 0);
	glBegin(GL_POLYGON);
	
	glColor3f(0, 1, 0);
	glVertex2f(def.left+defX, def.bottom);      //Left - Bottom 
	glVertex2f(def.right+ defX, def.bottom);
	glVertex2f(def.right+ defX, def.top);
	glVertex2f(def.left+ defX, def.top);
	glEnd();
	glFlush();
}



	

void Display() {
	float theta;

	glClearColor(0.847059, 0.664706, 0.164706, 1); //Background Color
	glClear(GL_COLOR_BUFFER_BIT);

	//THE SEA
	glPushMatrix();
	glColor3f(0, 0.8, 1);
	glBegin(GL_QUADS);
	glVertex3f(0,250, 0);
	glVertex3f(500,250, 0);
	glVertex3f(500,200, 0);
	glVertex3f(0,200, 0);
	glEnd();
	glPopMatrix();

	//SHARK
	glPushMatrix();
	glColor3f(0.137255, 0.137255, 0.006863);
	glBegin(GL_TRIANGLES);
	glVertex3f(0+shark, 210, 0);
	glVertex3f(50+shark, 210, 0);
	glVertex3f(0+shark, 240, 0);
	if (shark+25 < 500) {
		shark += 2;
	}
	else
	{
		shark = 0;
	}
	glEnd();
	glPopMatrix();

	if (!ended) {
	if (playerturn == 0) {
		glColor3f(1, 1, 1);
		print(180, 230, "left player turn");
	}
	else
	{
		glColor3f(1, 1, 1);
		print(180, 230, "right player turn");

	}
	glColor3f(1, 1, 1);
	print(pp1, pp2, z);


	

	//THE WALL
	glPushMatrix();
	glColor3f(1, 0, 0);
	glBegin(GL_QUAD_STRIP);
	glVertex3f(250, 0, 0);
	glVertex3f(270, 0, 0); 
	glVertex3f(250, 140, 0);
	glVertex3f(270, 140, 0);
	glEnd();
	glPopMatrix();
	
	



	//THE DEFENDER
	glPushMatrix();
	if (!defender_hit) {


		if (defender_visible) {
			if (defX < 500) {
				DrawRectangle(d);
				defX += 2;
			}
			else
			{
				defX = 1;
			}
		}
	}
	else
	{
		
	}
	glPopMatrix();
	

	//1ST PLAYER   
	glLineWidth(3);
	glColor3f(1,1,1);

	//1ST PLAYER HEAD
	glPushMatrix(); 
	glTranslated(0, right, 0);
	glBegin(GL_POLYGON);
	for (int i = 0; i < 360; i++)
	{
		theta = i * 3.142 / 180;


		glVertex2f(5 * cos(theta) + 30, 5 * sin(theta) + 30);
	}
	
	glEnd();
	glPopMatrix();

	
	//1ST PLAYER LEGS
	glPushMatrix();
	glBegin(GL_LINES);
	glColor3f(0, 0, 0);
	glVertex2i(25, 15);
	glVertex2i(25, 5);
	glVertex2i(35, 15);
	glVertex2i(35, 5);
	glEnd();
	glPopMatrix();

	//1ST PLAYER SHORT
	glPushMatrix();
	glBegin(GL_POLYGON);
	glColor3f(0.196078, 0.8, 0.196078);
	glVertex2i(22, 15);
	glVertex2i(22, 10);
	glVertex2i(26, 10);
	glVertex2i(29, 15);
	glVertex2i(32, 10);
	glVertex2i(36, 10);
	glVertex2i(36, 15);
	glEnd();
	glPopMatrix();

	//1ST PLAYER HANDS 
	glPushMatrix();
	glBegin(GL_LINE_STRIP);
	glColor3f(0, 0, 0);
	glVertex2i(34, 20);
	glVertex2i(45, 20);
	glVertex2i(26, 20);
	glVertex2i(15, 20);
	glEnd();
	glPopMatrix();


	//1ST PLAYER BODY
	glPushMatrix();
	glBegin(GL_TRIANGLES);
	glColor3f(1, 0, 0);
	glVertex2f(30, 25);
	glVertex2f(20, 15);
	glVertex2f(40, 15);
	glEnd();
	glPopMatrix();

	//1ST PLAYER HEALTH BAR
	glPushMatrix();
	glBegin(GL_LINE_LOOP);
	glColor3f(1, 1, 1);
	glVertex2f(10, 240);
	glVertex2f(10, 245);
	glVertex2f(40, 245);
	glVertex2f(40, 240);
	glEnd();
	glPopMatrix();

	//1ST PLAYER HEALTH
	glPushMatrix();
	glBegin(GL_QUADS);
	glColor3f(1, 1, 0);
	glVertex2f(10.5, 240.4);
	glVertex2f(10.5, 244.5);
	glVertex2f(health1, 244.5);
	glVertex2f(health1, 240.4);
	glEnd();
	glPopMatrix();
	
	//1ST PLAYER POWER BAR
	glLineWidth(1);
	glPushMatrix();
	glBegin(GL_LINE_LOOP);
	glColor3f(1, 1, 1);
	glVertex2f(5,5);
	glVertex2f(10, 5);
	glVertex2f(10, 40);
	glVertex2f(5,40);
	glEnd();
	glPopMatrix();

	//1ST PLAYER power

	glPushMatrix();
	//glTranslated(0.0, move1, 0.0);
	glBegin(GL_QUADS);
	glColor3f(1, 1, 0);
	glVertex2f(5.3, move1);
	glVertex2f(9.7, move1);
	glVertex2f(9.7, 5.5);
	glVertex2f(5.3, 5.5);
	glEnd();
	glPopMatrix();
	
	//1ST PLAYER BULLET
	glPushMatrix();
	glTranslated(x, y, 0);
	if (b1) {
		glBegin(GL_LINE_LOOP);
		glColor3f(0, 0, 0);
		glVertex2f(25, 25);
		glVertex2f(35, 25);
		glVertex2f(35, 15);
		glVertex2f(25, 15);
		glEnd();
		glBegin(GL_QUADS);
		glVertex2f(25, 25);
		glVertex2f(35, 25);
		glVertex2f(35, 15);
		glVertex2f(25, 15);
		glEnd();
		}
	glPopMatrix();


	//2ND player 
	glPushMatrix();
	glLineWidth(3);
	//2ND PLAYER HEAD
	glPushMatrix();
	glColor3f(1, 1, 1);
	glTranslated(0, right2, 0);
	glBegin(GL_POLYGON);
	for (int i = 0; i < 360; i++)
	{	theta = i * 3.142 / 180;
		glVertex2f(5 * cos(theta) + 470, 5 * sin(theta) + 30);
	}
	glEnd();
	glPopMatrix();

	//2ND PLAYER HANDS  
	glPushMatrix();
	glBegin(GL_LINE_STRIP);
	glColor3f(0, 0, 0);
	glVertex2i(455, 20);
	glVertex2i(474, 20);
	glVertex2i(485, 20);
	glEnd();
	glPopMatrix();
	
	
	//2ND PLAYER BODY
	glPushMatrix();
	glBegin(GL_TRIANGLES);
	glColor3f(1, 0, 0);
	glVertex2f(470, 25);
	glVertex2f(460, 15);
	glVertex2f(480, 15);
	glEnd();
	glPopMatrix();
	
	//2ND PLAYER legs
	glPushMatrix();
	glBegin(GL_LINES);
	glColor3f(0,0,0);
	glVertex2i(465,15);
	glVertex2i(465,5);
	glVertex2i(475,15);
	glVertex2i(475,5);
	glEnd();
	glPopMatrix();

	//@ND PLAYER SHORT
	glPushMatrix();
	glBegin(GL_POLYGON);
	glColor3f(0.196078, 0.8, 0.196078);
	glVertex2i(463, 15);
	glVertex2i(463, 10);
	glVertex2i(468, 10);
	glVertex2i(471, 15);
	glVertex2i(474, 10);
	glVertex2i(478, 10);
	glVertex2i(478, 15);
	glEnd();
	glPopMatrix();


	//2ND PLAYER HEALTH BAR
	glPushMatrix();
	glBegin(GL_LINE_LOOP);
	glColor3f(1, 1, 1);
	glVertex2f(460, 240);
	glVertex2f(460, 245);
	glVertex2f(490, 245);
	glVertex2f(490, 240);
	glEnd();
	glPopMatrix();

	//2ND PLAYER HEALTH
	glPushMatrix();
	glBegin(GL_QUADS);
	glColor3f(1,1,0);
	glVertex2f(460.5, 240.4);
	glVertex2f(460.5, 244.5);
	glVertex2f(health2, 244.5);
	glVertex2f(health2, 240.4);
	glEnd();
	glPopMatrix();

	//2ND PLAYER POWER BAR
	glLineWidth(1);
	glPushMatrix();
	glBegin(GL_LINE_LOOP);
	glColor3f(1, 1, 1);
	glVertex2f(490, 5);
	glVertex2f(495, 5);
	glVertex2f(495, 40);
	glVertex2f(490, 40);
	glEnd();
	glPopMatrix();

	//2ND PLAYER POWER
	glBegin(GL_QUADS);
	glColor3f(1, 1, 0);
	glVertex2f(490.3, move2);
	glVertex2f(494.7, move2);
	glVertex2f(494.7, 5.5);
	glVertex2f(490.3, 5.5);
	glEnd();
	glPopMatrix();

	//2ND PLAYER BULLET
	glPushMatrix();
	glTranslated(x, y, 0);
	if(b2){
	glBegin(GL_LINE_LOOP);
	glColor3f(0, 0, 0);
	glVertex2f(465, 25);
	glVertex2f(475, 25);
	glVertex2f(475, 15);
	glVertex2f(465, 15);
	glEnd();
	glBegin(GL_QUADS);
	glVertex2f(465, 25);
	glVertex2f(475, 25);
	glVertex2f(475, 15);
	glVertex2f(465, 15);
	glEnd();
	}
	
	glPopMatrix();

	}
	//game is ended
	else {
	glColor3f(1, 1, 1);
	print(180, 230, "game is ended");
	glColor3f(1, 1, 1);
	print(180, 180, "click to start again");

	glColor3f(1, 1, 1);
	print(pp1, pp2, z);

	//THE WALL
	glPushMatrix();
	glColor3f(1, 0, 0);
	glBegin(GL_QUAD_STRIP);
	glVertex3f(250, 0, 0);
	glVertex3f(270, 0, 0);
	glVertex3f(250, 140, 0);
	glVertex3f(270, 140, 0);
	glEnd();
	glPopMatrix();


	//THE DEFENDER
	glPushMatrix();
	DrawRectangle(d);
	glPopMatrix();


	//1ST PLAYER   
	glLineWidth(3);
	glColor3f(1, 1, 1);

	//1ST PLAYER HEAD
	glPushMatrix();
	glBegin(GL_POLYGON);
	for (int i = 0; i < 360; i++)
	{
		theta = i * 3.142 / 180;


		glVertex2f(5 * cos(theta) + 30, 5 * sin(theta) + 30);
	}

	glEnd();
	glPopMatrix();

	glPushMatrix();
	//1ST PLAYER LEGS
	glBegin(GL_LINES);
	glColor3f(0, 0, 0);
	glVertex2i(25, 15);
	glVertex2i(25, 5);
	glVertex2i(35, 15);
	glVertex2i(35, 5);
	glEnd();
	glPopMatrix();

	//1ST PLAYER HANDS 
	glPushMatrix();
	glBegin(GL_LINE_STRIP);
	glColor3f(0, 0, 0);
	glVertex2i(34, 20);
	glVertex2i(45, 20);
	glVertex2i(26, 20);
	glVertex2i(15, 20);
	glEnd();
	glPopMatrix();


	//1ST PLAYER BODY
	glPushMatrix();
	glBegin(GL_TRIANGLES);
	glColor3f(1, 0, 0);
	glVertex2f(30, 25);
	glVertex2f(20, 15);
	glVertex2f(40, 15);
	glEnd();
	glPopMatrix();

	

	//1ST PLAYER POWER BAR
	glLineWidth(1);
	glPushMatrix();
	glBegin(GL_LINE_LOOP);
	glColor3f(1, 1, 1);
	glVertex2f(5, 5);
	glVertex2f(10, 5);
	glVertex2f(10, 40);
	glVertex2f(5, 40);
	glEnd();
	glPopMatrix();

	//1ST PLAYER power

	glPushMatrix();
	//glTranslated(0.0, move1, 0.0);
	glBegin(GL_QUADS);
	glColor3f(1, 1, 0);
	glVertex2f(5.3, 39.5);
	glVertex2f(9.7, 39.5);
	glVertex2f(9.7, 5.5);
	glVertex2f(5.3, 5.5);
	glEnd();
	glPopMatrix();




	//2ND player 
	glPushMatrix();
	glLineWidth(3);
	//2ND PLAYER HEAD
	glPushMatrix();
	glColor3f(1, 1, 1);
	glBegin(GL_POLYGON);
	for (int i = 0; i < 360; i++)
	{
		theta = i * 3.142 / 180;
		glVertex2f(5 * cos(theta) + 470, 5 * sin(theta) + 30);
	}
	glEnd();
	glPopMatrix();

	//2ND PLAYER HANDS  
	glPushMatrix();
	glBegin(GL_LINE_STRIP);
	glColor3f(0, 0, 0);
	glVertex2i(455, 20);
	glVertex2i(474, 20);
	glVertex2i(485, 20);
	glEnd();
	glPopMatrix();


	//2ND PLAYER BODY
	glPushMatrix();
	glBegin(GL_TRIANGLES);
	glColor3f(1, 0, 0);
	glVertex2f(470, 25);
	glVertex2f(460, 15);
	glVertex2f(480, 15);
	glEnd();
	glPopMatrix();

	//2ND PLAYER legs
	glPushMatrix();
	glBegin(GL_LINES);
	glColor3f(0, 0, 0);
	glVertex2i(465, 15);
	glVertex2i(465, 5);
	glVertex2i(475, 15);
	glVertex2i(475, 5);
	glEnd();
	glPopMatrix();

	//2ND PLAYER POWER BAR
	glLineWidth(1);
	glPushMatrix();
	glBegin(GL_LINE_LOOP);
	glColor3f(1, 1, 1);
	glVertex2f(490, 5);
	glVertex2f(495, 5);
	glVertex2f(495, 40);
	glVertex2f(490, 40);
	glEnd();
	glPopMatrix();

	//2ND PLAYER POWER
	glBegin(GL_QUADS);
	glColor3f(1, 1, 0);
	glVertex2f(490.3, 39.5);
	glVertex2f(494.7, 39.5);
	glVertex2f(494.7, 5.5);
	glVertex2f(490.3, 5.5);
	glEnd();
	glPopMatrix();
}



	glFlush();
}

void mou(int b, int s, int x, int y)
{
	if (ended == false) {
	if (b == GLUT_LEFT_BUTTON && s == GLUT_DOWN)
	{
		firing = true;
	}

	else if (b == GLUT_LEFT_BUTTON && s == GLUT_UP) {
		if (playerturn == 0) {
			b2 = false;
			firing = false;
			throw1 = true;
			if ((move1 <= 12.5) && (move1 > 5.5)) {

				p0[0] = 30;
				p0[1] = 20;

				p1[0] = 100;
				p1[1] = 100;

				p2[0] = 150;
				p2[1] = 150;

				p3[0] = 100;
				p3[1] = 40;

			}
			if ((move1 <= 19) && (move1 > 12.5)) {

				p0[0] = 30;
				p0[1] = 20;

				p1[0] = 150;
				p1[1] = 150;

				p2[0] = 200;
				p2[1] = 200;

				p3[0] = 250;
				p3[1] = 0;

			}
			if ((move1 <= 25) && (move1 > 19)) {

				p0[0] = 30;
				p0[1] = 20;

				p1[0] = 240;
				p1[1] = 200;

				p2[0] = 290;
				p2[1] = 250;

				p3[0] = 340;
				p3[1] = 0;

			}
			if ((move1 <= 33) && (move1 > 25)) {

				p0[0] = 30;
				p0[1] = 20;

				p1[0] = 100;
				p1[1] = 250;

				p2[0] = 350;
				p2[1] = 250;

				p3[0] = 450;
				p3[1] = 0;

			}
			if ((move1 <= 40) && (move1 > 33)) {

				p0[0] = 30;
				p0[1] = 20;

				p1[0] = 150;
				p1[1] = 250;

				p2[0] = 400;
				p2[1] = 250;

				p3[0] = 500;
				p3[1] = 0;
			}


		}

		if (playerturn == 1) {
			b1 = false;
			firing = false;
			throw2 = true;
			if ((move2 <= 12.5) && (move2 > 5.5)) {

				p0[0] = 30;
				p0[1] = 20;

				p1[0] = 100;
				p1[1] = 100;

				p2[0] = 150;
				p2[1] = 150;

				p3[0] = 100;
				p3[1] = 40;

			}
			if ((move2 <= 19) && (move2 > 12.5)) {

				p0[0] = 30;
				p0[1] = 20;

				p1[0] = 150;
				p1[1] = 150;

				p2[0] = 200;
				p2[1] = 200;

				p3[0] = 250;
				p3[1] = 0;


			}
			if ((move2 <= 25) && (move2 > 19)) {

				p0[0] = 30;
				p0[1] = 20;

				p1[0] = 240;
				p1[1] = 200;

				p2[0] = 290;
				p2[1] = 250;

				p3[0] = 340;
				p3[1] = 0;

			}
			if ((move2 <= 33) && (move2 > 25)) {

				p0[0] = 30;
				p0[1] = 20;

				p1[0] = 100;
				p1[1] = 250;

				p2[0] = 350;
				p2[1] = 250;

				p3[0] = 450;
				p3[1] = 0;

				//if ((health1-5.5) > 5.5) {
				//	health1 = health1 - 5.5;
				//}
				//else {
				////prints game over player 2 is the winner
				//}

			}
			if ((move2 <= 40) && (move2 > 33)) {

				p0[0] = 30;
				p0[1] = 20;

				p1[0] = 150;
				p1[1] = 250;

				p2[0] = 400;
				p2[1] = 250;

				p3[0] = 500;
				p3[1] = 0;
			}

		}

	}
	}
else
	{
	if (b == GLUT_LEFT_BUTTON && s == GLUT_DOWN) {}
	else if (b == GLUT_LEFT_BUTTON && s == GLUT_UP) {
		ended = false;
	}
	}
}


void time(int v)//timer animation function, allows the user to pass an integer valu to the timer function.
{
	if (!ended) {
	
	if (firing == true) {
		if (playerturn == 0) {
			if(move1<39.5){
			move1+=2;
			}
		}
		else
		{
			if (move2 < 39.5) {
				move2 += 2;
			}
		}
	}
	else
	{
		if (playerturn == 0) {
			if (throw1 == true) {
				if (t < 2) {
					int* p = bezier(t, p0, p1, p2, p3);
					x = p[0];
					y = p[1];

					
					t += 0.1;
					if ((x+25>d.left+defX)&&(x+35<=d.right + defX)&&(y+15>=d.bottom)&&(y+25<d.top))
					{
			
							defender_hit = true;
							b1 = false;
							t = 2;
							
						}
					else if ((p1[0] == 150)&&(p1[1] == 150)&&(x >= 230)&&(x < 270)) {

						b1 = false;
						t = 2;

					}
					else if ((p3[0]==450)&&(p3[1]==0)&&(x>450)&&(x<490) )
					{
						if (health2 - 1.75> 460.5) {
						health2=health2-1.75;
						right2 = -10;
						}
						else
						{
							ended = true;
							pp1 = 100;
							pp2 = 150;
							ended = true;
							z = "the winner";


						}
					}
				}
				else
				{
					right2 = 0;
					t = 0;
					x = 0;
					y = 0;
					move1 = 5.5;
					throw1 = false;
					playerturn = 1;
					firing = false;
					b1 = false;
					b2 = true;
				}
			}
		}
		else
		{
		if (throw2 == true) {
			if (t < 2) {
				int* p = bezier(t, p0, p1, p2, p3);
				x = -p[0];
				y = p[1];
				t += 0.1;
				if ((465+x>d.left + defX)&&(x+475<=d.right + defX)&&(y+15>=d.bottom)&&(y+25<d.top))
				{
					defender_hit = true;
					b2 = false;
					t = 2;

				}
				else if ( (x <= -180) && (x>-300) && (p1[0]== 150) && (p1[1] == 150 )) {
					t = 3;

				}

				
				else if ((p3[0] == 450) && (p3[1] == 0) && (x < -450) && (x > -490))
				{
					if (health1 - 1.75 > 5.5) {
						health1 = health1 - 1.75;
						right = - 10;

					}
					else
					{
						t = 2;

						ended = true;
						pp1 = 350;
						pp2 = 150;
						z = "the winner";

					}
				}
			}


			else {
				right = 0;
				x = 0;
				y = 0;
				t = 0;
				move2 = 5.5;
				throw2 = false;
				playerturn = 0;
				firing = false;
				b2 = false;
				b1 = true;

			}
		}
		}
		}
		}
else
	{
	x = 0;
	y = 0;
	t = 0;
	move1 = 5.5;
	move2 = 5.5;
	defX = 1;
	throw2 = false;
	playerturn = 0;
	firing = true;
	b2 = false;
	b1 = true;
	health1 = 40;
	health2 = 490;
	
	defender_hit = false;
	defender_visible = true;

	}

	

	glutTimerFunc(80, time, 0);
	glutPostRedisplay(); 		
	defender_visible = !defender_visible;
	defender_hit = false;
	


}
void main(int argc, char** argr) {
	glutInit(&argc, argr);


	glutInitWindowSize(500, 250);
	glutInitWindowPosition(150, 150);
	p0[0] = 30;
	p0[1] = 20;

	p1[0] = 100;
	p1[1] = 250;

	p2[0] = 350;
	p2[1] = 250;

	p3[0] = 470;
	p3[1] = 20;
	glutCreateWindow("Control");
	glutDisplayFunc(Display);
	glutTimerFunc(0, time, 0);
	glutMouseFunc(mou);
	glutInitDisplayMode(GLUT_SINGLE | GLUT_RGB);
	glClearColor(0.0f, 0.0f, 0.0f, 0.0f);
	gluOrtho2D(0.0, 500, 0.0, 250);

	glutMainLoop();//don't call any method after this line as it will not be reached.
}

