# CasinoGame.cpp
#include <iostream>
#include <string>
#include <fstream>
using namespace std;

void createAcc(){
    string login;
    cout << "Create login: "; cin >> login; cout << endl;
    ifstream file;
    file.open(login + ".txt");
    while(file){
        cout << "There exist such an account" << endl;
        cout << "To enter new login, type (1)" << endl;
        cout << "To go to main menu, type (2)" << endl;
        int x;
        cin >> x;
        if(x == 1){
            createAcc();
            return;
        }
        else{
            cout << "Account wasn't created" << endl;
            cout << endl;
            return;
        }
    }
    string password;
    cout << "Create password: "; cin >> password; cout << endl;
    string balance;
    cout << "Enter Initial balance: "; cin >> balance; cout << endl;
    fstream new_file;
    new_file.open(login + ".txt",ios::out);
    new_file << login << endl;
    new_file << password << endl;
    new_file << balance << endl;
    new_file.close();
    cout << "Account created" << endl;
    cout << endl;
}
void replenishTheBalance(){
    string login;
    cout << "Enter login: "; cin >> login; cout << endl;
    ifstream file;
    file.open(login + ".txt");
    while(!file){
        cout << "The login is wrong" << endl;
        cout << "To try again, type (1)" << endl;
        cout << "To go to main menu, type (2)" << endl;
        int x;
        cin >> x;
        if(x == 1){
            replenishTheBalance();
            return;
        }
        else{
            return;
        }
    }
    file.close();
    string password;
    cout << "Enter password: "; cin >> password; cout << endl;
    ifstream File;
    File.open(login + ".txt");
    string pw;
    File >> pw;
    //cout << pw << endl;
    File >> pw;
    //cout << pw << endl;
    if(pw != password){
        while(pw != password){
            cout << "Entered password is incorrect" << endl;
            cout << "To try again, type (1)" << endl;
            cout << "To go to main menu, type (2)" << endl;
            int x;
            cin >> x;
            if(x == 1){
                cout << "Enter password: "; cin >> password; cout << endl;
            }
            else{
                return;
            }
        }
    }
    string balance;
    cout << "Enter balance that you want to replenish: "; cin >> balance; cout << endl;
    string bl;
    File >> bl;
    int amount = stoi(bl);
    amount = amount + stoi(balance);
    File.close();
    ofstream f(login + ".txt");
    f.close();
    fstream F;
    F.open(login + ".txt",ios::out);
    F << login << endl;
    F << password << endl;
    balance = to_string(amount);
    F << balance << endl;
    F.close();
    cout << "You successfully replenished your balance" << endl;
}
void play(){
    string login;
    cout << "Enter login: "; cin >> login; cout << endl;
    ifstream file;
    file.open(login + ".txt");
    if(!file){
        cout << "Such login doesn't exist" << endl;
        cout << "To try again, type (1)" << endl;
        cout << "To go to main menu, type (2)" << endl;
        int x;
        cin >> x;
        if(x == 1){
            play();
            return;
        }
        else{
            return;
        }
    }
    string password;
    cout << "Enter password: "; cin >> password; cout << endl;
    string pw;
    file >> pw;
    file >> pw;
    if(pw != password){
        while(pw != password){
            cout << "Entered password is incorrect" << endl;
            cout << "To try again, type (1)" << endl;
            cout << "To go to main menu, type (2)" << endl;
            int x;
            cin >> x;
            if(x == 1){
                cout << "Enter password: "; cin >> password; cout << endl;
            }
            else{
                return;
            }
        }
    }
    string balance;
    file >> balance;
    file.close();
    cout << "Account activated" << endl;
    cout << "Your balance is: " + balance << endl;
    int bl = stoi(balance);
    while(bl > 0){
        cout << "Your balance is: " << bl << endl;
        cout << "To continue, type (1)" << endl;
        cout << "To stop, type (2)" << endl;
        int x;
        cin >> x;
        if(x == 1){
            cout << "Select any number from 1 to 10" << endl;
            int y;
            cin >> y;
            int random = (rand()%10) + 1;
            if(random == y){
                cout << "Congratulations your number is super lucky, your balance has increased now by 500 tenge" << endl;
                bl = bl + 500;
            }
            else{
                cout << "Unfortunately this number was not that lucky, your balance decreased now by 50 tenge" << endl;
                bl = bl - 50;
            }
        }
        else{
            ofstream File(login + ".txt");
            File.close();
            fstream F;
            F.open(login + ".txt",ios::out);
            F << login << endl;
            F << password << endl;
            balance = to_string(bl);
            F << balance << endl;
            F.close();
            return;
        }
    }
    ofstream File(login + ".txt");
    File.close();
    fstream F;
    F.open(login + ".txt",ios::out);
    F << login << endl;
    F << password << endl;
    balance = to_string(bl);
    F << balance << endl;
    F.close();
    cout << "You lost your money, please replenish your balance to continue to play" << endl;
    cout << endl;
}
int main(){
    cout << "Select option (1-4):" << endl;
    cout << "(1)Play" << endl;
    cout << "(2)Create account" << endl;
    cout << "(3)Replenish the balance" << endl;
    cout << "(4)Exit" << endl;
    int x;
    cin >> x;
    if(x == 1){
        play();
        main();
    }
    else if(x == 2){
        createAcc();
        main();
    }
    else if(x == 3){
        replenishTheBalance();
        main();
    }
    else if(x == 4){
        return 0;
    }
}
