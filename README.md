# Voleyball
#include <iostream>
#include <fstream>
#include <string>
#include <clocale>


using namespace std;


void log(int whowiner, int  way, int  player) {
 
    ofstream result("logs.txt", ios::app);

    string record = " победила команда - ";
    string method;
    
    if (way == 1) {
        method = "атака";
    }else if(way == 2){
        method = "блок";
    }else if(way == 3){
        method = "подача";
    }else if(way == 4){
        method = "ошибка";
    }
    record += to_string(whowiner) + ", действие - " + method + ", игрок - " + to_string(player);
    result << record << endl;
    result.close();
       
}


void zamena(int* command) {
    ofstream result("logs.txt",ios::app);
    int zamena;
    int nakogo;
    string selection;
    bool player = true;
    int i = 0;
    
    do {

       cout << "кого вы хотите заменить - ";
    cin >> zamena;

            for ( i = 0; i < 6; i++) {

            if (command[i] == zamena) {

                player = false;

                break;
            }
        }
        if (player) {
            cout << "неверный игрок!" << endl;
        }

    } while (player);

    cout << "кем вы хотите заменить - ";
    cin >> nakogo;

    cout << "подтвердите E - ";
    cin >> selection;

    if (selection == "E") {
        command[i] = nakogo;
        cout << endl;
    }
    result << "замена игрока - " + to_string(zamena) + "на игрока - " + to_string(nakogo) << endl;
    result.close();
}



void perexod(int* oneteam) {
    int sdvig = oneteam[5];
    for (int i = 5; i > 0; i--) {
        oneteam[i] = oneteam[i - 1];

    }
    oneteam[0] = sdvig;


}


void zadacha2(int* oneteam, int* twoteam)
{
    for (int i = 0; i < 3; i++) {
        cout << oneteam[i] << " ";

    }

    cout << "    ";

    for (int i = 0; i < 3; i++) {
        cout << twoteam[i] << " ";

    }
    cout << endl;

    for (int i = 5; i > 2; i--) {
        cout << oneteam[i] << " ";

    }

    cout << "    ";
    for (int i = 5; i > 2; i--) {
        cout << twoteam[i] << " ";

    }

    cout << endl;

}

void zadacha1(int* oneteam, int* twoteam) {
    ofstream result("Bd.txt");
    int win1 = 0;
    int win2 = 0;
    int whowiner = 0;
    
    while (win1 < 3 && win2 < 3) {
        int way = 0;
        int player = 0;
        int lastwiner = 0;
        int count1 = 0;
        int count2 = 0;
        bool player1 = true;
        while ((count1 < 25 && count2 < 25) or (count1 - count2 < 2 or count2 - count1 < 2)) {

            printf("Счет матча %d (%d) – %d (%d)  .\n", win1, count1, win2, count2);

            zadacha2(oneteam, twoteam);

            cout << "кто победит 1 команда или команда 2,\n3 - замена - ";
            cin >> whowiner;
            cout << endl;



            if (whowiner == 3) {
                int command = 0;

                cout << "какая команда? - ";
                cin >> command;

                if (command == 1) {
                    zamena(oneteam);
                }
                else {
                    zamena(twoteam);
                }
                continue;
            }


            cout << "выйграл \n 1-Атака \n 2-Блок \n 3-Подача \n 4-Ошибка\n";
            cin >> way;
            if (way != 4) {
                do {
                    cout << " кто выйграл розыгрыш - ";
                    cin >> player;
                    if (whowiner == 1) {
                        for (int i = 0; i < 6; i++) {

                            if (oneteam[i] == player) {

                                player1 = false;

                                break;
                            }
                        }
                    }
                    else if (whowiner == 2) {
                        for (int i = 0; i < 6; i++) {

                            if (twoteam[i] == player) {

                                player1 = false;
