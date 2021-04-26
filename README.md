# Chapter-6-Lab-Functions-Computer-Information-
This program calculates the price of a computer by asking the user for it's specifications.





#include <string>
#include <iostream>
using namespace std;

//Funtion prototypes
void getComputerInformation(double &, double &, double &, bool &);
double computerPriceCalculation(double &, double &, double &, bool &);
void displayComputerInformation(double &, double &, double &, bool &);
bool erroneousUserInputs(double);

int main()
{
    //Variable declaration
    double processorSpeed;
    double storageCapacity;
    double memoryAmount;
    bool touchScreenChoice = 0;
    char additionalComputers;
    
    //Tell the user what the program does.
    cout << "This program calculates the price of a computer.\n";
    
    //Loop to allow for additional computers to be created
    do
    {
            //Function calls
            getComputerInformation(processorSpeed, storageCapacity, memoryAmount, touchScreenChoice);     //Gets the users input
            displayComputerInformation(processorSpeed, storageCapacity, memoryAmount, touchScreenChoice); //Displays the computer info
            
            //Ask the user if the wish to create another computer
            cout << "Would you like to create another computer? Y/N ";
            cin >> additionalComputers;
    }       while (additionalComputers == 'y' || additionalComputers == 'Y');
    
    return 0;
}

//***********************************************************
// Definition of getComputerInformation. This function gets
// information from the user about the computer specs they
// want. The parameters processorSpeed, storageCapacity,
// memoryAmount, and touchScreenChoice are reference
// variables that refer to these choices.
//***********************************************************

void getComputerInformation (double &processorSpeed,
                             double &storageCapacity,
                             double &memoryAmount,
                             bool &touchScreenChoice)
{
    //Variable declaration
    char touchScreen;
    
    //Request and store users inputs and validate them by calling the validateUserInputs function
    cout << "\nEnter a processor speed: ";
    cin >> processorSpeed;
    while (erroneousUserInputs(processorSpeed))
        {
            cout << endl << "ERROR You must enter a positive value! " << endl ;
            cout << "Please reenter a processor speed: " ;
            cin >> processorSpeed;
            erroneousUserInputs(processorSpeed);
        }
    
    cout << endl << "Enter a storage capacity: ";
    cin >> storageCapacity;
    while (erroneousUserInputs(storageCapacity))
        {
            cout << endl << "ERROR You must enter a positive value! " << endl ;
            cout << "Please reenter a storage capacity: ";
            cin >> storageCapacity;
            erroneousUserInputs(storageCapacity);
        }

    cout << endl << "Enter an amount of memory: ";
    cin >> memoryAmount;
    while (erroneousUserInputs(memoryAmount))
        {
            cout << endl << "ERROR You must enter a positive value! " << endl ;
            cout << "Please reenter an amount of memory: ";
            cin >> memoryAmount;
            erroneousUserInputs(memoryAmount);
        }
    
    cout << endl <<"Would you like a touch screen? Y/N ";
    cin >> touchScreen;
    if (touchScreen == 'y' || touchScreen == 'Y')
        touchScreenChoice = true;
    if (touchScreen == 'n' || touchScreen == 'N')
        touchScreenChoice = false;
}

//***********************************************************
// Definition of erroneousUserInputs. This function checks
// if the users input is INVALID (less than or equal to 0)
// and if it is INVALID it returns a boolean value of 'true'
// or '1'. The parameter inputToValidate is a local variable.
// It's value is tested to for erroneous user input (!>0).
//***********************************************************

bool erroneousUserInputs (double inputToValidate)
{
    if (inputToValidate <= 0)
        return true;
    else
        return false;
}

//***********************************************************
// Definition of computerPriceCalculation. This function
// calculates the price of the computer based on the
// preferences indicated by the user and returns the this
// value which is locally stored in the variable
// totalComputerPrice. The parameters processorSpeed,
// storageCapacity, memoryAmount, and touchScreenChoice
// are reference variables that refer to these preferences.
//***********************************************************

double computerPriceCalculation (double &processorSpeed,
                               double &storageCapacity,
                               double &memoryAmount,
                               bool &touchScreenChoice)
{
    //Constant variable definitions
    double const BASE_COST = 150;
    double const MARK_UP = .75;
    double const BASE_PROCESSOR_SPEED = 2;
    double const UPGRADED_STORAGE = 500;
    double const UPGRADED_STORAGE_COST = 45;
    double const BASE_MEMORY_AMOUNT = 4;
    double const UPGRADED_MEMORY_COST = 50;
    double const UPGRADED_PROCESSOR_COST = 50;
    
    //Variable definitions
    double processorCost = 0;
    double storageCost = 0;
    double memoryCost = 0;
    double touchScreenCost = 0;
    double totalComputerPrice;
    
    //Conditional statements
    if (processorSpeed > BASE_PROCESSOR_SPEED)
    {
        processorCost = (processorSpeed - BASE_PROCESSOR_SPEED) * UPGRADED_PROCESSOR_COST;
    }

    if (storageCapacity >= UPGRADED_STORAGE)
    {
        storageCost = UPGRADED_STORAGE_COST;
    }
    
    if (memoryAmount > BASE_MEMORY_AMOUNT)
    {
        memoryCost = (memoryAmount - BASE_MEMORY_AMOUNT) * UPGRADED_MEMORY_COST;
    }
    
    if (touchScreenChoice)
    {
        touchScreenCost = 60;
    }
    
    //Calculations of the total cost and price of the computer
    double totalComputerCost = BASE_COST + processorCost + storageCost + memoryCost + touchScreenCost;
    totalComputerPrice = (totalComputerCost * MARK_UP) + totalComputerCost;
    
    return totalComputerPrice;
}

//***********************************************************
// Definition of displayComputerInformation. This function
// displays the configuration of the computer that the user
// has chosen which included the parameters listed:
// processorSpeed, storageCapacity, memoryAmount, and
// touchScreenChoice. The parameters processorSpeed,
// storageCapacity, memoryAmount, and touchScreenChoice are
// reference variables. The values in these reference
// variables reference the options chosen by the user for
// their computer.
//***********************************************************

void displayComputerInformation (double &processorSpeed,
                                 double &storageCapacity,
                                 double &memoryAmount,
                                 bool &touchScreenChoice)
{
    //Variable declaration
    string stringTouchScreen;
    
    //Conditional statements
    if (touchScreenChoice)
        stringTouchScreen = "Yes";
    else
        stringTouchScreen = "No";
    
    //Output statements to display specs and call upon computerPriceCalculation's return value to display the total price
    cout << endl << "Your computer's configuration will be:\n";
    cout << "______________________________________\n";
    cout << endl << "Processor Speed:                 " << processorSpeed << " GHz " << endl;
    cout << endl << "Storage Capacity:                " << storageCapacity << " GB " << endl;
    cout << endl << "Memory (RAM):                    " << memoryAmount << " GB " << endl;
    cout << endl << "Touch Screen:                    " << stringTouchScreen << endl;
    cout << endl << "The total computer price is:     $" << computerPriceCalculation (processorSpeed, storageCapacity, memoryAmount, touchScreenChoice) << endl << endl;
}

