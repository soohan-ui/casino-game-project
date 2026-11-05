#include<stdio.h>
#include <stdlib.h>
#include <time.h>

int winCount = 0;
int loseCount = 0;
int drawCount = 0;

int drawCard(void)
{
    //2부터 11까지 무작위 숫자
    return rand() % 10 + 2;
}
//블랙잭
int blackjack(int coin){
    //변수 선언
    int player;
    int dealer;
    int card;
    int bet;
    char choice;

    //코인 베팅
    printf("\n현재 보유 코인: %d\n", coin);
    printf("베팅할 코인을 입력하세요: ");
    scanf("%d", &bet);

    if (bet <= 0 || bet > coin)
    {
        printf("베팅 금액이 올바르지 않습니다.\n");
        return coin;
    }

    //카드 두 장 뽑기
    player = drawCard() + drawCard();
    dealer = drawCard() + drawCard();

    //게임 시작
    printf("게임 시작! 당신은 두 장의 카드를 받았습니다.\n");
    printf("당신의 카드 합계: %d\n", player);
    printf("딜러의 카드 합계: %d\n\n", dealer);

    //플레이어 턴
    while (1)
    {
        printf("카드를 더 받으시겠습니까? (y/n): ");
        scanf(" %c", &choice);

        if (choice == 'n' || choice == 'N')
        {
            break;
        }

        if (choice != 'y' && choice != 'Y')
        {
            printf("y 또는 n을 입력하세요.\n");
            continue;
        }

        //카드 추가
        card = drawCard();
        player += card;

        printf("당신은 %d을(를) 받았습니다.\n", card);
        printf("당신의 카드 합계: %d\n", player);
        printf("딜러의 카드 합계: %d\n\n", dealer);

        //21점 초과
        if (player > 21)
        {
            printf("21점을 초과했습니다. 딜러가 승리했습니다!\n");

            coin -= bet;
            loseCount++;

            printf("현재 보유 코인: %d\n", coin);

            return coin;
        }
    }

    //딜러 턴
    while (dealer < 17)
    {
        card = drawCard();
        dealer += card;

        printf("딜러는 %d을(를) 받았습니다.\n", card);
        printf("당신의 카드 합계: %d\n", player);
        printf("딜러의 카드 합계: %d\n\n", dealer);
    }

    //결과 출력하기
    if (dealer > 21)
    {
        printf("딜러가 21점을 초과했습니다. 당신이 승리했습니다!\n");
        coin += bet;
        winCount++;
    }
    else if (player > dealer)
    {
        printf("당신이 승리했습니다!\n");
        coin += bet;
        winCount++;
    }
    else if (player < dealer)
    {
        printf("딜러가 승리했습니다!\n");
        coin -= bet;
        loseCount++;
    }
    else
    {
        printf("무승부입니다!\n");
        drawCount++;
    }

    printf("현재 보유 코인: %d\n", coin);

    return coin;
}
//바카라
int baccarat(int coin){}
//주사위
int diceGame(int coin){}
//룰렛
int roulette(int coin){}
//슬롯머신
int slotMachine(int coin){}
//하이로우
int highLow(int coin){}
//게임전적
void showStats(int coin)
{
    int total;

    total = winCount + loseCount + drawCount;

    printf("\n========== 게임 전적 ==========\n");
    printf("총 게임 횟수: %d\n", total);
    printf("승리: %d회\n", winCount);
    printf("패배: %d회\n", loseCount);
    printf("무승부: %d회\n", drawCount);

    if (total > 0)
    {
        printf("승률: %.1f\n", (double)winCount / total * 100);
    }
    else
    {
        printf("아직 플레이한 게임이 없습니다.\n");
    }

    printf("현재 보유 코인: %d\n", coin);
    printf("===============================\n");
}

int main(){
int coin = 1000;
int choice;

srand((unsigned int)time(NULL));

while(1){
    printf("\n\n==========casino==========");
    printf("\n\n 현재 보유 코인:%d\n",coin);
    printf("1. 블랙잭\n");
    printf("2. 바카라\n");
    printf("3. 주사위\n");
    printf("4. 돌림판\n");
    printf("5. 슬롯머신\n");
    printf("6. 하이로우\n");
    printf("7. 게임 전적 확인\n");
    printf("0. 프로그램 종료\n");
    printf("==============================\n");


printf("게임을 선택하세요:");
    scanf("%d",&choice);


switch(choice){
   case 1:
   coin = blackjack(coin);
   break;

   case 2:
   coin = baccarat(coin);
   break;
   
   case 3:
   coin = diceGame(coin);
   break;

   case 4:
   coin = roulette(coin);
   break;

   case 5:
   coin = slotMachine(coin);
   break;

   case 6:
   coin = highLow(coin);
   break;

   case 7:
   showStats(coin);
   break;

   case 0:
   printf("게임을 종료합니다");
   return 0;

   default:
   printf("잘못된 번호 입니다.");
   break;
}

}




}

