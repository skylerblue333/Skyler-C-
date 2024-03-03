
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

