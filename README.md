/* Summarize the project and what problem it was solving.

This program carries out a range of operations to overall be an item-tracking program. This works by analyzing the text records made through that day. I assume these are text files made or taken from some database. It makes sense of the data in specific ways based on the functionality and design I incorporated. 


What did you do particularly well?

I think I made the entire project particularly well, based on the instructions I was given. But overall you could say I like the menu options displayed to the user to choose from. 

Where could you enhance your code? How would these improvements make your code more efficient, secure, and so on?

I could enhance my code like everyone through industry best practices and continue to make my code more readable and maintainable. This could be done and continued to improved on by practicing on more projects and working with others.

Which pieces of the code did you find most challenging to write, and how did you overcome this? 

I think the most challenging part was the data file creation, to backup accumulated data. This is one of the first times I have implemented that in my code. 

What tools or resources are you adding to your support network?

I am now adding GitHub and connections to others as a tool and a support network. 

What skills from this project will be particularly transferable to other projects or coursework?

I think all skills used and thus improved on can be particularly transferable to any project. If I had to select one it would be my new skill to create a data file. With the functionality to backup my accumulated data. 

How did you make this program maintainable, readable, and adaptable?

I did this by using industry best practices such as in-line comments and appropriate naming conventions, to enhance readability and maintainability. *\



#include <iostream>
#include <fstream>
#include <string>
#include <map>

using namespace std;

// function to read file and pop frequency map
void readDataFromFile(map<string, int>& frequencyMap, const string& filename) {
	ifstream inputFile(filename);
	if (!inputFile.is_open()) {
		cout << "There is an error opening the file." << filename << endl;
		exit(EXIT_FAILURE);
	}

	string item;
	int count;
	while (inputFile >> item >> count) {
		frequencyMap[item] = count;
	}

	inputFile.close();
}

// fucnction to print frequency of the items 
void printFrequency(const map<string, int>& frequencyMap) {
	cout << "Frequency of the items." << endl;
	for (const auto& pair : frequencyMap) {
		cout << pair.first << " " << pair.second << endl;
	}
}

//function to print histogram
void printHistogram(const map<string, int>& frequencyMap) {
	cout << "Histogram:" << endl;
	for (const auto& pair : frequencyMap) {
		cout << pair.first << " ";
		for (int i = 0; i < pair.second; ++i) {
			cout << "*";
		}
		cout << endl;
	}
}

int main() {
	const string inputFilename = "CS210_Project_Three_Input_File.txt";
	map<string, int> frequencyMap;

	// read data from the file 

	readDataFromFile(frequencyMap, inputFilename);

	int choice;
	do {
		cout << "Menu Options:" << endl;
		cout << "1. Look up an item." << endl;
		cout << "2. Print frequency." << endl;
		cout << "3. print histogram." << endl;
		cout << "4. Exit." << endl;
		cout << "Enter menu choice to move foward: ";
		cin >> choice;

		switch (choice) {
		case 1: {
			string item;
			cout << "Enter the name of item to look it up: ";
			cin >> item;
			if (frequencyMap.find(item) != frequencyMap.end()) {
				cout << "Frequency of " << item << ": " << frequencyMap[item] << endl;
			} else {
				cout << "Item is not found in the system." << endl;
			}
			break;
		}
		case 2:
			printFrequency(frequencyMap);
			break;
		case 3:
			printHistogram(frequencyMap);
			break;
		case 4:
			cout << "Exiting the program." << endl;
			break;
		default:
			cout << "Invalid choice. Input a another choice." << endl;
		}
	} while (choice != 4);


// create backup file 
ofstream backupFile("frequency.dat");
if (backupFile.is_open()) {
	for (const auto& pair : frequencyMap) {
		backupFile << pair.first << " " << pair.second << endl;
	}
	backupFile.close();
	cout << "Backup file frequency.dat created." << endl;
} else {
	cout << "Error creating backup file." << endl;
}

return 0;
}

