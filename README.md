#include "stdafx.h"
#include <iostream>
#include <Windows.h>
#include <conio.h>

using namespace std;

bool fps;
int width = 40 - 1;
int height = 20 - 1;
int x = width / 2 - 1;
int y = height / 2 - 1;

int fruitX = rand() % width;
int fruitY = rand() % height;
int tailX[100];
int tailY[100];
int nTail;
enum eDiraction {STOP = 0, UP, DOWN, LEFT, RIGHT};
eDiraction dir;
int score = 0;

void Setup() {
	fps = false;
}

void Draw() {
	Sleep(1);
	system("cls");
	for (int i = 0; i < width; i++)
		cout << "#";
	cout << endl;

	for (int i = 0; i < height; i++) {
		for (int j = 0; j < width; j++) {
			if (j == 0 || j == width - 1)
				cout << "#";
			
			if (j == x && i == y)
				cout << "0";
			if (j == fruitX && i == fruitY)
				cout << "F";
			else {
				bool print = false;
				for (int k = 0; k < nTail; k++) {
					if (tailX[k] == j && tailY[k] == i) {
						print = true;
						cout << "o";
					}
				}
				if(!print)
				cout << " ";
			}
			
		} 
		cout << endl;
	} 

    for (int i = 0; i < width; i++)
		cout << "#";
	cout << endl;

	cout << "Score: " << score;
}

void Input() {
	if(_kbhit())
		switch (_getch())
		{
		case 'a':
			dir = LEFT;
			break;
		case 'd':
			dir = RIGHT;
			break;
		case 's':
			dir = DOWN;
			break;
		case 'w':
			dir = UP;
			break;
		
		}

}

void Logic() {
	int prevX = tailX[0];
	int prevY = tailY[0];
	int prev2X, prev2Y;
	tailX[0] = x;
	tailY[0] = y;
	for (int i = 1; i < nTail; i++) {
		prev2X = tailX[i];
		prev2Y = tailY[i];
		tailX[i] = prevX;
		tailY[i] = prevY;
		prevX = prev2X;
		prev2Y = prev2X;

	}
	switch (dir)
	{
	
		break;
	case UP:
		y--;
		break;
	case DOWN:
		y++;
		break;
	case LEFT:
		x--;
		break;
	case RIGHT:
		x++;
		break;

		
	
	}
	if (x == -3) {
		x = width - 3;
	}
	else if (x == width) {
		x = 0 - 3;
	}
	else if (y == -3) {
		y = height;
	}
	else if (y == height) {
		y = 0 - 3;
	}
		

				
			
		

	if (x == fruitX && y == fruitY) {
		score += 10;
	    fruitX = rand() % width;
	    fruitY = rand() % height;
		nTail++;

	}

}

int main() {
	
	while (!fps) {
		Draw();
		Input();
		Logic();

	}
	
	return 0;
}
