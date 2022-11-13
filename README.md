#include <bits/stdc++.h>
using namespace std;
class Client;
class BankAccount;
class SavingsBankAccount;
class Bankapplication;

class Client
{
private:
    string name,address,phone_number;
    BankAccount* ptr1;
    SavingsBankAccount* ptr2;
public:
    Client (){};
    Client(string str,string addr,string phone)
    {
        name=str;
        address=addr;
        phone_number=phone;
    };
    Client(BankAccount &acc)
    {
        ptr1=&acc;
    };
    Client(SavingsBankAccount &acc){
        ptr2=&acc;
    };

};

class BankAccount
{
protected:
    string id;
    double balance;
    Client* cptr;
public:
    //BankAccount(string Id)
    BankAccount(double b){
        balance=b;
    }
    BankAccount(Client& c){
        cptr=&c;
    }
    BankAccount(){
        id="FCAI-";
        balance=0.0;
    }
    void SetBalance(double b){
        balance=b;
    }
    double GetBalance(){
        return balance;
    }
    void SetID(string str){
        id=str;
    }

    string GetID(){
        return id;
    }

    double withdraw(double money)
    {
        if (balance>=money)
        {
            balance-=money;
        }
        else
            cout<<"insufficient money,your account has "<<balance<<" only"<<endl;
        return balance;
    }
    void deposit(double money)
    {
        balance+=money;
    }
};

class SavingsBankAccount: public BankAccount
{
private:
    double minibalance;
public:
    using BankAccount::BankAccount;
    SavingsBankAccount()
    {
        minibalance=1000.0;
    }
    SavingsBankAccount(double b)
    {
        if (b>=minibalance)
            balance=b;
        else
            cout<<"minimum balance is 1000"<<endl;
    }
    double Getmini()
    {
        return minibalance;
    }
    double withdraw(double money)
    {
        if ((balance-money)>=minibalance)
            balance-=money;
        else
            cout<<"withdrawing is below the minimum balance"<<endl;
        return balance;
    }
    void deposit(double money)
    {
        if (money>=100)
            balance+=money;
        else
            cout<<"you can ONLY put 100 pounds or more as a deposit"<<endl;
    }
};

class Bankapplication
{
    int choice;
public:
    ofstream& newacc(){
        ofstream file;
        file.open("Banksystem.txt", ios::app);
        //Client person;
        string name,address,phone;
        cout<<"Please Enter Client Name"<<endl;
        cin>>name;
        file<<name;
        cout<<"Please Enter Client Address"<<endl;
        cin>>address;
        file<<address;
        cout<<"Please Enter Client Phone"<<endl;
        cin>>phone;
        file<<phone;
        Client person(name,address,phone);
        BankAccount B1(person);
        int flag;
        int static no=1;
        cout<<"What Type of Account Do You Like? (1) Basic (2) Saving : Type 1 or 2"<<endl;
        cin>>flag;
        if(flag==1){
            //BankAccount B1;
            cout<<"Please Enter the Starting Balance"<<endl;
            double bal;
            cin>>bal;
            string id;
            //id = B1.GetID();
            id.push_back(no+'0');
            B1.SetID(id);
            file << id;

            file<<bal;
            B1.SetBalance(bal);
            //BankAccount(balance);
            //BankAccount(person);
        }
        else if(flag==2){
            //SavingsBankAccount B2;
            cout<<"Please Enter the Starting Balance at least 1000$"<<endl;
            double  balance;
            cin>>balance;
            SavingsBankAccount B2(person);
            B2.SetBalance(balance);

            string id;
            id = B1.GetID();
            id.push_back(no+'0');
            B1.SetID(id);
            file<<balance;
        }
        file.close();
        return file;

    }
    void list_clients(){}

    void displaymenu(){
        cout<<"Welcome to FCAI Banking Application\n"
              "1. Create a New Account\n"
              "2. List Clients and Accounts\n"
              "3. Withdraw Money\n"
              "4. Deposit Money\n"
              "Please Enter Choice =========>"<<endl;
        cin>>choice;
        if(choice==1){
            newacc();
        }
        if(choice==2){

        }
        if(choice==3){

        }
        if(choice==4){

        }
    }

};

int main() {
    Bankapplication b;
    b.newacc();
    return 0;
}
