# Atividade-44

#include <stdio.h>
#include <stdlib.h>

#define N 8

int moveX[8] = {2, 1, -1, -2, -2, -1, 1, 2};
int moveY[8] = {1, 2, 2, 1, -1, -2, -2, -1};

void imprimirTabuleiro(int tabuleiro[N][N]) {
    for (int x = 0; x < N; x++) {
        for (int y = 0; y < N; y++) {
            printf("%2d ", tabuleiro[x][y]);
        }
        printf("\n");
    }
}

int ehValida(int x, int y, int tabuleiro[N][N]) {
    return (x >= 0 && x < N && y >= 0 && y < N && tabuleiro[x][y] == -1);
}

int resolverTour(int x, int y, int movei, int tabuleiro[N][N]) {
    if (movei == N*N)
        return 1;

    for (int k = 0; k < 8; k++) {
        int proximoX = x + moveX[k];
        int proximoY = y + moveY[k];
        if (ehValida(proximoX, proximoY, tabuleiro)) {
            tabuleiro[proximoX][proximoY] = movei;
            if (resolverTour(proximoX, proximoY, movei + 1, tabuleiro))
                return 1;
            else
                tabuleiro[proximoX][proximoY] = -1; 
        }
    }
    return 0;
}

int main() {
    int tabuleiro[N][N];

    for (int x = 0; x < N; x++)
        for (int y = 0; y < N; y++)
            tabuleiro[x][y] = -1;

    int inicialX = 0;
    int inicialY = 0;
    tabuleiro[inicialX][inicialY] = 0; 

    if (resolverTour(inicialX, inicialY, 1, tabuleiro)) {
        imprimirTabuleiro(tabuleiro);
    } else {
        printf("Solução não encontrada.\n");
    }

    return 0;
}
