# Object-Oriented-Programming-Notes

//  OOP-Notes

//  This notes I took helped me understand OOP
//  It includes some basic explanations of how some concepts work as well as some (not very good) examples.

#include <iostream>//basic library
#include <string>//string library
#include <fstream>//I/O library
using namespace std; //BAD PRACTICE!!!!!!!!!!!!!!!!

//---------------Basic Classes-------------------//

class BasicClass {

//basic class named BasicClass

public:      //access specifier: anything outside the class can access the attributes of the class

    //Class Attributes

    int myNumb; //integer type
    float myFloat; //float type
    string myString; //string type
    bool myBool; //boolean type
};

//---------------Basic Classes With Methods-------------------//


class ClassWithMethod { 

//a class with a basic method called ClassWithMethod

public:
    void aMethod() {//method deffintion
        //a method is a fiunction inside a class and can access variables inside the class

        cout << "\n" << "Hello from a method!!" << endl; //The method displays a sentence
    }


};

// methods can also be defined outside the class the following way:
// inside the class: declare the function and its inputs
// outside the class: (function type) className :: mthodName()
// the :: is used to define the scope of the function



//Class called coffee with a method that takes parameters
//and a method definition outside the class

class Coffee {

public:

    void PriceMethod(float price);//declaration of Price Method
};

void Coffee::PriceMethod(float price) { //deffinition of Price method

    cout << "\n" << "The Price of coffee is: $" << price << "\n" << endl;
}


//---------------Constructors-------------------//

//Consructors are special methods that are called when an object is created

class Kava {

public:

    string name = "n/a";
    float price = 0;

    Kava(string kName, float kPrice);//constructor declaration

};

Kava::Kava(string kName, float kPrice) {//constructor definition

    name = kName;
    price = kPrice;

    cout << "\n" << "Name: " << name << endl
        << "The price is: $" << price << endl
        << "Bula!!!" << endl;


}


//---------------Access Specifiers--------------//

//Access specifier define how the attributes and methods of the class can be access
//Public: members are accessible from outside the class
//Private: members cant be accessed from outside (only through methods)
//Protected: members can be accessed only by inherated classes

class protecClass {

private:

    int x;

public:

    int y;


};

//---------------Encapsulation--------------//


//Encapsulation protects data from users by using privates attributes
//encapsulation uses getters and setters
//setters/mutators can defined and interact with the private attrs
//getters display the information

class BetterKava {

private:

    double price;//default attr for price
    

public:

    string description;//default attr for string
    BetterKava();//default constructor
    void  setter(double p, string s);//getter and setter declarations
    float getter();

};

BetterKava::BetterKava() {

//the constructor will always display the messeage and set dfault values to the attr

    cout << "\n" << "Hello from a constructor!!! this is an improved kava class!" << endl;

    price = 0.0;
    description = "n/a";

}


void BetterKava::setter(double p, string s) {//using the getter() method we can muttate the default attrs

    price = p;
    description = s;

}

float BetterKava::getter() {

//setter allows to diplay the private attr from outside

    return price;
}


 //---------------Inheritance--------------------------------------------------------//
 
 
 //We can pass attributes and methods from one class to another
 //Inheritance allow us to reuse attributes and methods
 //Child/Derived class: the class that is borrowing from other classes
 //Parent/Base class: The class that is borrowed from

class Drinks {

//Let drinks be our parent class

public:

    string Name;
    double Price;
    
    Drinks(){
        cout <<"\n\n"<<"Hello from the construstor inside the parent class named Drinks"<<endl;
        Name = "n/a";
        Price = 0;
    }
};

//drinks is broad enough to be a parent
//there can be different drink types: wines, beers, and coctails
//let say we want to make a derived class from drinks just for beers
//all the drived classes will use the name, price and the default constructor from drinks

class Beer: public Drinks{

//Beer is a derived class from Drinks

public:

    string Brewery;//It wouldnt make sense to use brewery in the child because only beers are made in breweries
    
    string Beerkind;//While kind can be broad too, Beerkind refers to IPA, Wheat Beer, Dark Lager, etc
    
    Beer();
    void BeerSetter(string n,double p, string brw, string brk);//declaration of a setter method
    void BeerDisplay();
    
    
};

Beer::Beer(){
    
    cout<<"Hello from the child default constructor from the child class named Beer"<<endl;
    Brewery = "n/a";
    Beerkind = "n/a";
    
}


void Beer::BeerSetter(string n,double p, string brw, string brk ){//The efinition of the setter method from the child class: Beer
    
    Name = n;
    Price = p;
    Brewery = brw;
    Beerkind = brk;
    
}

void Beer::BeerDisplay(){//BeerDisplay method outputs the parent and child attr
    
    cout<<"\n\n"<<"Name: "<<Name<<endl<<"Price: $"<<Price<<endl
    <<"Brewery: "<<Brewery<<endl<<"Kind: "<<Beerkind<<endl;
    
}

//we can have a multi-level inheretance; Cider is the granchild of Drinks and Child of beers
//A more ideal example would be having the following classes: Beer derived from alcoho, and alcohol be derived from Drinks

class Cider:public Beer{

public:

    string Region;//cider has the attributes of its parents and itself
    Cider();//it has its own constructor
    void CiderSetter(string n,double p, string brw, string brk, string reg);//its own setter that passes all the attr
    void CiderDisplay();//its own diplay method that displays all attr
    
};

Cider::Cider(){
    
    cout<<"Hello from the grandchild constructor from the class cider"<<endl;
    Region = "n/a";
    
}

void Cider::CiderSetter(string n,double p, string brw, string brk, string reg){
    
    Name = n;
    Price = p;
    Brewery = brw;
    Beerkind = brk;
    Region = reg;
}

void Cider::CiderDisplay(){
    
    cout<<"\n\n"<<"Name: "<<Name<<endl<<"Price: $"<<Price<<endl
    <<"Brewery: "<<Brewery<<endl<<"Kind: "<<Beerkind<<endl
    <<"Region: "<<Region<<endl;
}

//We can also do multi-inheratence
//instead of having one base class we can have two and have a combination of all of methods and attributes
//lets create a new class named alcohol

class Alcohol{

public:

    double alchLvl;
    Alcohol();
    void AlcoholSetLevel(double al);
};

Alcohol::Alcohol(){
    cout << "\nHello from the alcohol class"<<endl;
}
void Alcohol::AlcoholSetLevel(double al){
    alchLvl = al;
}

//now lets create a new class that will multiple inheretance


class Bar: public Alcohol, public Cider{//bar will have attr from alcohol class and cider class
    
public:
    
    Bar(){
        cout<<"\n\nHello from the multiple inhertance class named Bar"<<endl;
    }
    
    void DisplayBar(){
        
        //we can see that bar does not only has the attr from its parents
        //but because Cider is a grandchild, Bar has the attr of Cider's parent and grandparent
        
        cout<<"\n\n"<<"Name: "<<Name<<endl<<"Price: $"<<Price<<endl
        <<"Brewery: "<<Brewery<<endl<<"Kind: "<<Beerkind<<endl
        <<"Region: "<<Region<<endl<<"Alcohol Level: %"<<alchLvl<<endl;
        
    }
};


//---------------Inheritance With Access Specifiers--------------------------------------------------------//


//Child classes can access private attributes of other classes
//This is called the protected access specifier

class Company {

//company is a class with protected attr

public:

    string compName;
    string address;
    Company();
protected:

    string depName;
    int noOfEmpl;//number of employees
    float earnings;
};

Company::Company(){

//default constructor definition

    cout<<"\nHello from the Company parent class construct"<<endl;
    compName = "n/a";
    address = "n/a";
    depName = "n/a";
    noOfEmpl = 0;
    earnings = 0;
}


//Lets create a class departmaent that can access the protected class from company

class DepartmentInfo: public Company{
public:

    DepartmentInfo();//Default Constructor
    DepartmentInfo(string comN, string addi, string depn, int noOfEm, float earn);//constructor
    
};

DepartmentInfo::DepartmentInfo(){
    
    cout<<"\nCompany name: "<<compName<<endl<<"Address: "<<address<<endl
    <<"Department Name: "<<depName<<endl<<"Number of employees: "<<noOfEmpl<<endl
    <<"earnings: "<<earnings<<endl;
    
    
}
DepartmentInfo::DepartmentInfo(string comN, string addi, string depn, int noOfEm, float earn){
    
    //DepartmentInfo can set and read the attr from company
    
    cout<<"\nHello from the Department info child class"<<endl;
    compName = comN;
    address = addi;
    depName = depn;
    noOfEmpl = noOfEm;
    earnings = earn;
    
    cout<<"\nCompany name: "<<compName<<endl<<"Address: "<<address<<endl
    <<"Department Name: "<<depName<<endl<<"Number of employees: "<<noOfEmpl<<endl
    <<"earnings: "<<earnings<<endl;
    
}

//---------------Polymorphism-------------------------------------------------------------------------//


//Polymorphism means "many forms" and the concept is based around the use of inheretance to perform differen taks
//The goal of polymorphism is to reuse code
//lets make a new example
   
class TechCompany{

public:

    string name;
    string ceo;
    string description;
    TechCompany();
    
protected:

    double earnings;
};
TechCompany::TechCompany(){

    name="no info";
    ceo="no info";
    description="no info";
    earnings = 0;
    
}


class SocialMedia: public TechCompany{

public:

    int numbOfUser;
    SocialMedia();
    SocialMedia(string na, string ce, string des, double earn, int nouser);
};

SocialMedia::SocialMedia(){

    numbOfUser = 0;
    
    cout<<"\nName: "<<name<<endl<<"CEO: "<<ceo<<endl<<"Description: "<<endl
    <<"No of active users: " <<numbOfUser<<endl<<"Value: $"<<earnings<<endl;
}

SocialMedia::SocialMedia(string na, string ce, string des, double earn, int nouser){

    name=na;
    ceo=ce;
    description=des;
    earnings = earn;
    numbOfUser = nouser;
    
    cout<<"\nName: "<<name<<endl<<"CEO: "<<ceo<<endl<<"Description: "<<description<<endl
    <<"No of active users: " <<numbOfUser<<endl<<"Value: $"<<earnings<<endl;
}






int main() { 

//REMEMBER!!!!!! ALWAYS USE MAIN(){}


    //---------------------------Basic Classes and objects-------------------------------------------//






    cout << "\n" << "BASIC CLASSES AND OBJECTS" << "\n" << endl;

    //Bsic class deffinition

    BasicClass MyObj;//An object

    //accessing and deffining attributes

    MyObj.myNumb = 1;
    MyObj.myFloat = 1.5;
    MyObj.myString = "Hello World";
    MyObj.myBool = true; // true = 1 false = 0;

    //Displaying the values of MyObj Object

    cout << "\n" << "Displaying MyObj attributes" << "\n" << endl;

    cout << MyObj.myNumb << endl
        << MyObj.myFloat << endl
        << MyObj.myString << endl
        << MyObj.myBool << endl;


    //Another object named wine that consit of
    //the name (string), price(float), quantity(int), is it imported(bool)

    BasicClass wine;

    wine.myNumb = 3;
    wine.myFloat = 8.99;
    wine.myString = "Red Wine";
    wine.myBool = false;

    //Display of the wine object based on myClass

    cout << "\n" << "Object named wine has information for red wine: the name (string), price(float), quantity(int), is it imported(bool)" << endl;

    cout << "\n" << endl
        << "Name: " << wine.myString << endl
        << "Price: " << "$" << wine.myFloat << endl
        << "Quantity: " << wine.myNumb << endl
        << "imported?: " << wine.myBool << endl;


    //-------------------------Methods---------------------------------------------//






    cout << "\n\n" << "BASIC METHODS" << "\n\n" << endl;


    //creattion of an object with a method

    cout << "\n" << "The following sentence comes from a method which is a function inside a class: " << endl;

    ClassWithMethod basicMethods; //creation of the obj
    basicMethods.aMethod(); //method call

    cout << "\n\n" << "The following sentence comes from a method which is a function inside an object named bean: " << endl;

    //creation of an object with a method that takes parameters
    Coffee bean;//object called bean
    bean.PriceMethod(2.55);//method call with a parameter



    //-------------------------Constructors---------------------------------------------//



    cout << "\n\n" << "CONSTRUCTORS" << "\n" << endl;

    cout << "\n\n" << "The following objects are created with a constructor: " << endl;

    //creation of an object with a constructor

    Kava black("Black", 7.00);//calls constructor
    Kava white("White", 7.00);//calls constructor



    //-------------------------Access Specifier---------------------------------------------//




    protecClass ProtObj; //creates an object with private attribute

    ProtObj.y = 10;
    //ProtObj.x = 11 creates an error becuse x is private

    cout << "\n\n" << "ProtObj has 2 attributes: x=11(private), y=10(public)" << endl
        << "x cannot be dispayed because it will create errors" << endl;

    cout <<"\n"<<"y:"<< ProtObj.y << endl;
    cout << "x: Displaying will create errors" << endl;



    //---------------Encapsulation--------------------------------------------------------//
    
    //Encapsulation makes use of setters and getters to access the private attr in a class

    cout << "\n\n" << "Encapsulation uses setters to set private and public attr, and setter to return priavate attr" << endl;

    BetterKava stone;
    stone.setter(6.99, "Strongest There is!");
    cout << "\nStone:\n" << endl << "Price: $" << stone.getter() << endl << "Descrip: " << stone.description << endl;
    
    cout<<"\n\n"<<"Wow has uninitialized attr, the constructor gives its default vaules of 0 and n/a"<<endl;

    BetterKava wow;
    cout << "\nwow:\n" << endl << "Price: $" << wow.getter() << endl << "Descrip: " << wow.description << endl;
    
    
    //---------------Inheritance--------------------------------------------------------//
    
    cout<<"\n\nINHERETANCE"<<endl;
    
    //The Beer pruple haze makes use of the setter and diplay metod to define the attr and siplay them
    
    cout<<"\n\nThe following displays the oncept of inheretance with parent and child: "<<endl;
    
    Beer PurpleHaze;
    PurpleHaze.BeerSetter("PurpleHaze", 10.99, "Abita", "Lager");
    PurpleHaze.BeerDisplay();
    
    //The Beer Amber has not set values therefore it will display the values set by the constructors
    
    Beer Amber;
    Amber.BeerDisplay();
    
    //We can use multi-level inheratance to pass different attr
    //In this particular example we made Drink the parent, Beer the child, and Cider the grand-child
    //A better example would be having Cider derived from alcohol and alcohol being derived from drinks
    
    cout<<"\n\nThe following displays the oncept of inheretance with parent, child and grandchild: "<<endl;
    
    Cider AngryOrch;
    AngryOrch.CiderSetter("Crisp Apple", 12.99, "Angry Orchard", "Cider", "North America");
    AngryOrch.CiderDisplay();
    
    Cider MadApple;
    MadApple.CiderDisplay();
   
    //We can also use multiple inheretance to get a combination of all attr
    //The class Bar has 2 parents: Alcohol, and Cider
    //Because Cider is a grandchild, Bar will have all the attr and methods from all of Cider's parents
    
    cout<<"\n\nThe following shows a combination of multi-level inheretance"<<endl
    <<"and multiple inheretance: "<<endl;
    
    Bar DrunkMan;
    DrunkMan.CiderSetter("Corona", 12.99, "Cervecería Modelo", "Pale Lager", "Mexico");
    DrunkMan.AlcoholSetLevel(4.6);
    DrunkMan.DisplayBar();//the output can show us which classes are processed first
    
    //---------------Inheritance with access specifier--------------------------------------------------------//
    
    cout<<"\n\nINHERETANCE WITH ACCESS SPECIFIER"<<endl;
    
    //A child can access its parent protected information
    //in this example we used the company class that has protected attr
    //and its departmentinfo child that will access and define such info
    //(string comN, string addi, string depn, int noOfEm, float earn)
    
    cout<<"\n\nThe following example shows how a child class can access private memebers: "<<endl;
    
    DepartmentInfo Sales("BigBigCompany","3303 some street, NY", "Sales", 30, 31.50);
    DepartmentInfo Sales2;
    
    //---------------Polymorphism-------------------------------------------------------------------------//
    //Evrything on these notes lead to polymorphism (many forms)
    //The goal of polymorphism and OOP as a whole is the re-use of code
    //polymorphysim is very valuable in team projects
    
    cout << "\n\nThe following example is not much different from the other examples"<<endl
    <<"we use polymorphism to create a child class with reaused attr from the parent"<<endl;
    //string na, string ce, string des, double earn, int nouser
    SocialMedia Social1("Tinder", "Elie Seidman", "Dating app", 10, 50);
    SocialMedia Social2("Twitter", "Elon Musk", "Living hell, i fucking hate twitter", 2, 1);


    return 0;
}
