# Order Overlook
#### Video Demo:  <URL https://youtu.be/9zJBWNbsyCM>
#### Description:
#### Introduction:
Order Overlook is a project made entirely with python that **writes and analises data from a csv file based on the inputs provided by the user**. It was designed based on a problem that I faced while working at a cake factory in my city, in which the owners were not so satisfied about not knowing precisely relevant information from their own factory. Based on that, **this program aims to promote centered and unified data in a csv file, making it possible to retrieve valued information, such as the turnover of the products and their contribution margin.**

#### Order class:
The program's functionality is supported by a class called *Order*, also developed in the main file *project.py*. In order to work properly, it requires 2 args (name, delivery_address) and 3 kwargs (cake=0, dark_pot=0, white_pot=0):

- **args**
    - **name:**
        - Refers to the client's company name, in order to keep track of whose order a specific order is;
        - This is a required field, if nothing is assigned to that, the program will raise a ValueError;
        - By default, it capitalizes the first letter of the words provided through title().
    - **delivery:**
        - Refers to the location of the client's company;
        - That is also a required field, but it must be a value compatible with the places that the cake factory actually delivers - ["Aguas Claras",
            "Lago Sul",
            "Sudoeste",
            "Asa Sul",
            "Asa Norte",
            "Jardim Botanico",
            "Lago Norte",
            "Guara",] -, otherwise, a ValueError will be raised;
        - By default, it also capitalizes the first letter of the words provided through title().
- **kwargs**
    - **cake:**
        - Refers to how many whole cakes are being ordered;
        - By default, its value is zero and if the number is not an integer or a positive value, it will raise a ValueError.
    - **dark_pot:**
        - Refers to how many pots with tradicional dark chocolate are being ordered;
        - By default, its value is zero and if the number is not an integer or a positive value, it will raise a ValueError.
    - **white_pot:**
        - Refers to how many pots with white chocolate are being ordered;
        - By default, its value is zero and if the number is not an integer or a positive value, it will raise a ValueError.

#### Order Class functions
In order to work properly, the Order class was built with some functions, such as:

- **init(self, name, delivery_address, cake, dark_pot, white_pot):**
    - That function handles the initialization of the class, assigning the values provided to the proper instance variables.
- **specific getters and setters for each value provided:**
    - Check if the arguments passed are actually valid before being assigning it to the instance variables.
- **str(self):**
    - Formats the class to a string "name: {?}, address: {?}, cakes: {?}, dark pot: {?}, white pot: {?}", where "?" represent placeholders form the actual values.
- **get(cls):**
    - A class method that handles getting the requested information in order to create a Order class;
    - It checks for valid information for each value, reprompting the user through a loop as long as the value is invalid.

#### Main Function
The main function of the program was written to get the current date formatted as "YYYY-mm-dd", aiming to name the csv file with the actual date from the time they are being inputted. With that said, it assumes all the orders provided at once are from the current day. After that, it goes through a loop, continuously getting the orders with Order.get() as long as the user keeps inputing "y" or "yes" - case insensitively- when the question "Would you like to register another order? (y/n): " appears. For each order inputted, main() also open a file "{current date}.csv" - as mentioned before, naming it with the current date-, and writes down all the orders, line by line. After that, when the loop breaks, by receiving a "n" or "no" - case insensitively- to that same question, it calls the following functions, detailed in the *Custom Functions* section:

- **analysis():**
    - Analyze data from a csv document.
- **doc():**
    - Write a csv file with the analysis made.
- **compare():**
    - Compare results from two different csv files.
- **comp_analysis():**
    - Compare two different days (csv files).

> These last two functions were elaborated as additional functionality (optional) to the program, designed to be used in particular ocasions, so that the main program still works using just the first two.

#### Custom Functions
The program contains four functions other than main(), which are the following:

- **analysis(str, cake=70, dark=15, white=15):**
    - It analyses data from a csv document, returning a dictionary with the total quantity, turnover and contribution margin for each product listed;
    - The default prices are cake=70 for whole cakes, dark=15 for dark pots and white=15 for white pots, but can be changed by the user.
- **doc(date, dic):**
    - It writes a new csv file with the dictionary returned from analysis() with the name "results_{specific date}.csv";
    - Since each csv file is named with the current date of the day it was written, doc requests a date as the first argument, formatted as "YYYY-mm-dd";
        - The function uses regular expressions to check if the input is valid. If the document doesn't exist, or the argument isn't written correctly, it will exit with an error message.
    - The other argument is the dictionary returned from analysis.
- **compare(str1, str2):**
    - That function allows the user to compare two different csv files written by main();
    - It was thought to be used as the reversed functionality of the doc() function, now retrieving two dictionaries (instead of writing) from the csv files requested, one for each, through a tuple.
- **comp_analysis(dic1, dic2):**
    - It can be used to compare two different csv files, taking as arguments the dictionaries inside the tuple returned from compare();
    - It calculates variables related to quantity, turnover and contribution margin, returning a formatted string with the totals, the mean and the standard deviation for each.

#### Tests
The tests located at *test_project.py* focus on testing functions related to the class itself and also some custom functions:

- **Order class tests:**
    - **test_Order_init():**
        - Check if Order initializes correctly when changing default values;
        - Check if Order initializes correctly with the default values;
        - Check ValueError raises: if name is not provided or delivery_address is not listed.
    - **test_Order_str():**
        - Check the format of the Order class when str() gets called.
    - **test_analysis():**
        - Check function with default price values;
        - Check function when changing default values.
    - **test_compare():**
        - Check if the operations made when comparing the two csv files match the return value.
    - **test_comp_analysis():**
        - Check if the operations made when comparing the two dictionaries match the return value and if the str is correctly formatted.

#### Code Display:
The document's organization was based on the requirements provided on the Final Project. Inside the project's directory, the following can be found:

- **Single Files:**
  - **project.py:** that's where the main python code works to make possible all the features presented so far. That's where the Order class, the main function and the custom functions are written;
  - **test_project.py:** where all the test functions were elaborated;
  - **2023-01-10.csv and 2023-01-11:** examples of csv files written by the program in order to center all the orders of one specific day;
  - **results_2023-01-10.csv and results_2023-01-11.csv:** examples of csv files written by the program with the whole data analysis from the day specified in the file name;
  - **README.md:** the current file, wrote to explain the whole idea behind the project.