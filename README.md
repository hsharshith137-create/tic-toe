#include<stdio.h>
int main()
{
    char ttt[9]={' ',' ',' ',' ',' ',' ',' ',' ',' '};
    char move='x', em=' ';
    int pos;

    for(int i=1;i<=9;i++)
    {
        printf("enter your move ");
        scanf("%d",&pos);

        // FIX 1: validate range
        if(pos < 0 || pos > 8)
        {
            printf("Invalid position! Use 0-8.\n");
            i--; 
            continue;
        }

        // FIX 2: check BEFORE writing
        if(ttt[pos] != em)
        {
            printf("already taken\n");
            i--;                     // do NOT count this as a move
            continue;
        }

        ttt[pos] = move;             // safe to place now

        // FIX 3: correct %C → %c
        printf("%c|%c|%c\n", ttt[0], ttt[1], ttt[2]);
        printf("-+-+-\n");
        printf("%c|%c|%c\n", ttt[3], ttt[4], ttt[5]);
        printf("-+-+-\n");
        printf("%c|%c|%c\n", ttt[6], ttt[7], ttt[8]);

        // WIN CHECKS
        if(ttt[0]==move && ttt[1]==move && ttt[2]==move) break;
        if(ttt[3]==move && ttt[4]==move && ttt[5]==move) break;
        if(ttt[6]==move && ttt[7]==move && ttt[8]==move) break;

        if(ttt[0]==move && ttt[3]==move && ttt[6]==move) break;
        if(ttt[1]==move && ttt[4]==move && ttt[7]==move) break;
        if(ttt[2]==move && ttt[5]==move && ttt[8]==move) break;

        if(ttt[0]==move && ttt[4]==move && ttt[8]==move) break;
        if(ttt[2]==move && ttt[4]==move && ttt[6]==move) break;

        // switch player
        if(move=='x') move='o';
        else move='x';
    }

    // WIN or TIE OUTPUT
    if(
        (ttt[0]==move && ttt[1]==move && ttt[2]==move) ||
        (ttt[3]==move && ttt[4]==move && ttt[5]==move) ||
        (ttt[6]==move && ttt[7]==move && ttt[8]==move) ||
        (ttt[0]==move && ttt[3]==move && ttt[6]==move) ||
        (ttt[1]==move && ttt[4]==move && ttt[7]==move) ||
        (ttt[2]==move && ttt[5]==move && ttt[8]==move) ||
        (ttt[0]==move && ttt[4]==move && ttt[8]==move) ||
        (ttt[2]==move && ttt[4]==move && ttt[6]==move)
      )
    {
        printf("%c wins, game over\n", move);
    }
    else
    {
        printf("It's a tie!\n");      // FIX 4: tie message
    }

    return 0;
}
