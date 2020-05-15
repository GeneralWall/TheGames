#include "pch.h"
#include <iostream>
#include <malloc.h>
#include <ctime>
#include <conio.h>
#include <vector>
#include <algorithm>

using namespace std;
bool gameover = false;

enum Move {
	UP,
	DOWN,
	RIGHT,
	LEFT,
	NOTHING
};

void makenewnum(int **f, bool &gameover); // prototype

int** createField() {																		// ОСНОВНЫЕ ПРОБЛЕМЫ:
																							// Ошибка с Game Over
	int size = 4;																			// рэнд четверки

	int **f = new int *[size];

	for (int i = 0; i < size; i++) {

		f[i] = new int[size];

		for (int j = 0; j < size; j++) {

			f[i][j] = 0;
		}
	}
	makenewnum(f, gameover);

	return f;
}
void Show(int **f){

	int sizes = _msize(f) / sizeof(int);

	for (int i = 0; i < sizes; i++) {

		for (int j = 0; j < sizes; j++) {

			if (f[i][j] == 0) {
				cout << " " << "\t";
			}
			else
			cout << f[i][j] << "\t";
		}
		cout << endl << endl;
	}
}


void makenewnum(int **f, bool &gameover) {

	int lenght = _msize(f) / sizeof(int);
	int x, y, sumNum;
	int count = 0;
	bool GetFour = false; // // //

	vector<int> ofNums;

	for (int i = 0; i < lenght; i++) {        // СИЛЬНО БЬЕТ ПО ПРОИЗВОДИТЕЛЬНОСТИ  (для рэнда четверки
		for (int j = 0; j < lenght; j++) {
			if (f[i][j] >= 16) {
				GetFour = true;
				break;
			}
		}
	}

	while (true) {
		 y = rand() % lenght; //!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
		 x = rand() % lenght; //     !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

		 if (f[x][y] == 0) {
			 
			 if (GetFour) {
				 int rander = rand() % 100;
				 if (rander < 40) {
					 f[x][y] = 2;
				 }
				 else f[x][y] = 4;
			 }
			 else f[x][y] = 2;
			 break;
		 }
		 
		 sumNum = x * 10 + y;  //-------------- проверка на наличие комбинации в прошлом ---- и ---- проверка на конец игры
		 auto result = find(ofNums.begin(), ofNums.end(), sumNum);
		 if (result == ofNums.end()) {
			 ofNums.push_back(sumNum);
			 count++;
		 }

		 if (count == 15) {
			 gameover = true;
			 cout << "GAME OVER" << endl;
			 break;
		 }  //-------------------..--------------------..---------------------..-----------------------..--------------------
	}
}
void Input(Move &dure, bool &gameover) {

	if (_kbhit()) {

		switch (_getch())
		{
		case 'w':
			dure = UP;
			break;
		case 's':
			dure = DOWN;
			break;
		case 'a': 
			dure = LEFT;
			break;
		case 'd':
			dure = RIGHT;
			break;
		case 'r':
			gameover = true;
			break;
		}
	}
}



void Logic(Move &dur, int **f, bool &gameover) {

	int siize = _msize(f) / sizeof(int);        //-----> size <-----
	
	int rez = 0;
	int countSteps = 0; //  для подсчета смещений

	switch (dur)
	{
	case NOTHING:
		break;

	case LEFT:

		for (int i = 0; i < siize; i++) { 
			for (int j = 0; j < siize; j++) {
				for (int kam = j + 1; kam < siize; kam++) {

					if (f[i][kam] != 0 && f[i][kam] != f[i][j]) {
						break;
					}
					if (f[i][j] == f[i][kam]) {
						f[i][j] += f[i][kam];
						f[i][kam] = 0;
						break;
					}
				}
			}
		}
		for (int i = 0; i < siize; i++) {
			for (int ken = 0; ken < siize; ken++) {

				if (f[i][ken] == 0) {
					rez++;
				}
				if (f[i][ken] != 0) {

					if (rez != 0) {
						f[i][ken - rez] = f[i][ken];
						f[i][ken] = 0;

						countSteps++; // === === === === === ===
					}
				}
			}
			rez = 0;
		}
		if (countSteps != 0) {  // === === === ===
			makenewnum(f, gameover);
		}
		countSteps = 0; ///////// === ==== ===
		dur = NOTHING;
		break;

	case RIGHT:

		for (int i = 0; i < siize; i++) {
			for (int j = siize - 1; j >= 0; j--) { //          ----     ----   reworking...
				for (int kam = j - 1; kam >= 0; kam--) {

					if (f[i][kam] != 0 && f[i][kam] != f[i][j]) {
						break;
					}
					if (f[i][j] == f[i][kam]) {
						f[i][j] += f[i][kam];
						f[i][kam] = 0;
						break;
					}
				}
			}
		}
		for (int i = 0; i < siize; i++) {
			for (int ken = siize - 1; ken >= 0; ken--) { // reworking...

				if (f[i][ken] == 0) {
					rez++;
				}
				if (f[i][ken] != 0) {

					if (rez != 0) {
						f[i][ken + rez] = f[i][ken];
						f[i][ken] = 0;

						countSteps++; // === === ===
					}
				}
			}
			rez = 0;
		}

		if (countSteps != 0) { //=======
			makenewnum(f, gameover);
		}
		countSteps = 0; // ========
		dur = NOTHING;
		break;

	case UP:

		for (int j = 0; j < siize; j++) {
			for (int i = 0; i < siize; i++) {
				for (int kam = i + 1; kam < siize; kam++) {

					if (f[kam][j] != 0 && f[kam][j] != f[i][j]) {
						break;
					}
					if (f[i][j] == f[kam][j]) {
						f[i][j] += f[kam][j];
						f[kam][j] = 0;
						break;
					}
				}
			}
		}
		for (int j = 0; j < siize; j++) {
			for (int ken = 0; ken < siize; ken++) {

				if (f[ken][j] == 0) {
					rez++;
				}
				if (f[ken][j] != 0) {

					if (rez != 0) {
						f[ken - rez][j] = f[ken][j];  //   rework !!!warning...
						f[ken][j] = 0;

						countSteps++; // === ==== ===
					}
				}
			}
			rez = 0;
		}

		if (countSteps != 0) { // === === ===
			makenewnum(f, gameover);
		}
		countSteps = 0; //=== ==== ===
		dur = NOTHING;
		break;

	case DOWN:
		for (int j = 0; j < siize; j++) {
			for (int i = siize - 1; i >= 0; i--) {
				for (int kam = i - 1; kam >= 0; kam--) {

					if (f[kam][j] != 0 && f[kam][j] != f[i][j]) {
						break;
					}
					if (f[i][j] == f[kam][j]) {
						f[i][j] += f[kam][j];
						f[kam][j] = 0;
						break;
					}
				}
			}
		}
		for (int j = 0; j < siize; j++) {
			for (int ken = siize - 1; ken >= 0; ken--) {

				if (f[ken][j] == 0) {
					rez++;
				}
				if (f[ken][j] != 0) {

					if (rez != 0) {
						f[ken + rez][j] = f[ken][j];  //   rework !!!warning...
						f[ken][j] = 0;

						countSteps++; // === === ===
					}
				}
			}
			rez = 0;
		}

		if (countSteps != 0) { //=== === ===
			makenewnum(f, gameover);
		}
		countSteps = 0; // === === ===
		dur = NOTHING;
		break;
	}
}



int main()
{
	srand(time(NULL)); // --------- --------- -------- ----------

	int **field = createField();

	Move duration = NOTHING;

	//bool gameover = false;
	while (!gameover) {

		system("cls");

		Input(duration, gameover);
		//if (duration == RIGHT) { // for TEST---
		//
		//	makenewnum(field, gameover);
		//	duration = NOTHING;
		//} //---
		Logic(duration, field, gameover);

		Show(field);
	}

	return 0;
}
