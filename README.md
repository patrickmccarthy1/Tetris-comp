# Tetris-comp
Tetris build 

#include <iostream>
#include <windows.h>
using namespace std;

wstring tetrino[7];
int nFieldWidth = 12;
int nFieldHeight = 18;
unsigned char *pField = nullptr;

int nScreenWidth = 80;
int nScreenHeight = 30;


int rotate(int px, int py, int r) {
	switch (r % 4)
	{
	case 0: return py * 4 + px;
	case 1: return 12 + py -(px * 4);
	case 2: return 15 - (py * 4) - px;
	case 3: return 3 - py + (px * 4);
	}
	return 0;
}

int main(){

	tetrino[0].append(L"..X.");
	tetrino[0].append(L"..X.");
	tetrino[0].append(L"..X.");
	tetrino[0].append(L"..X.");

	tetrino[1].append(L"....");
	tetrino[1].append(L".XX.");
	tetrino[1].append(L".XX.");
	tetrino[1].append(L"....");

	tetrino[2].append(L".XX.");
	tetrino[2].append(L"..X.");
	tetrino[2].append(L"..X.");
	tetrino[2].append(L"....");

	tetrino[3].append(L".XX.");
	tetrino[3].append(L".X..");
	tetrino[3].append(L".X..");
	tetrino[3].append(L"....");

	tetrino[4].append(L".X..");
	tetrino[4].append(L".XX.");
	tetrino[4].append(L"..X.");
	tetrino[4].append(L"....");

	tetrino[5].append(L"..X.");
	tetrino[5].append(L".XX.");
	tetrino[5].append(L".X..");
	tetrino[5].append(L"....");

	tetrino[6].append(L"....");
	tetrino[6].append(L"....");
	tetrino[6].append(L".XXX");
	tetrino[6].append(L"..X.");

	pField = new unsigned char[nFieldWidth*nFieldHeight];
	for (int x = 0; x < nFieldWidth; x++)
		for (int y = 0; y < nFieldHeight; y++)
			pField[y * nFieldWidth + x] = (x == 0 || x == nFieldWidth - 1 || y == nFieldHeight - 1) ? 9 : 0;

	wchar_t *screen = new wchar_t[nScreenWidth * nScreenHeight];
	for (int i = 0; i < nScreenWidth * nScreenHeight; i++) screen[i] = L' ';
	HANDLE hConsole = CreateConsoleScreenBuffer(GENERIC_READ | GENERIC_WRITE, 0, NULL, CONSOLE_TEXTMODE_BUFFER, NULL);
	SetConsoleActiveScreenBuffer(hConsole);
	DWORD dwBytesWritten = 0;

	bool bGameOver = false;

	while (!bGameOver) {

		for (int x = 0; x < nFieldWidth; x++)
			for (int y = 0; y < nFieldHeight; y++)
				screen[(y + 2) * nScreenWidth + (x + 2)] = L" ABCDEFG=#"[pField[y*nFieldWidth + x]];

		WriteConsoleOutputCharacter(hConsole, screen, nScreenWidth * nScreenHeight, { 0,0 }, &dwBytesWritten);
	}

	return 0; 
