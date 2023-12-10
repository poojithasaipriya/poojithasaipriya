#include <iostream>
#include <vector>
#include <string>
#include <fstream>
#include <iomanip>
#include <limits>

using namespace std;

struct Student {
    string name;
    vector<double> assignmentGrades;
    double finalGrade; // Added to store the final grade
};

double calculateFinalGrade(const vector<double>& assignmentGrades); // Function declaration

void addStudent(vector<Student>& students) {
    Student student;
    cout << "Enter student name: ";
    cin.ignore();
    getline(cin, student.name);

    cout << "Enter assignment grades (enter -1 to finish):\n";
    double grade;
    while (true) {
        cout << "Enter grade (-1 to finish): ";
        cin >> grade;

        if (grade == -1) break;
        else if (grade < 0 || grade > 100) {
            cout << "Invalid grade. Grades should be between 0 and 100." << endl;
            continue; // Ask for the grade again
        }

        student.assignmentGrades.push_back(grade);
    }

    // Calculate and store the final grade
    student.finalGrade = calculateFinalGrade(student.assignmentGrades);

    students.push_back(student);
}

double calculateFinalGrade(const vector<double>& assignmentGrades) {
    double total = 0.0;
    for (const double& grade : assignmentGrades) {
        total += grade;
    }
    return (total / assignmentGrades.size());
}

void displayStatistics(const vector<Student>& students) {
    if (students.empty()) {
        cout << "No students entered yet." << endl;
        return;
    }

    double totalFinalGrade = 0.0;
    double minGrade = students[0].finalGrade;
    double maxGrade = students[0].finalGrade;

    for (const Student& student : students) {
        double finalGrade = student.finalGrade;
        totalFinalGrade += finalGrade;

        if (finalGrade < minGrade) minGrade = finalGrade;
        if (finalGrade > maxGrade) maxGrade = finalGrade;
    }

    double averageGrade = totalFinalGrade / students.size();

    cout << "Statistics:\n";
    cout << "Total Students: " << students.size() << endl;
    cout << "Average Grade: " << fixed << setprecision(2) << averageGrade << endl;
    cout << "Minimum Grade: " << minGrade << endl;
    cout << "Maximum Grade: " << maxGrade << endl;
}

void exportReport(const vector<Student>& students, const string& filename) {
    ofstream outFile(filename);

    if (!outFile.is_open()) {
        cerr << "Error: Unable to open the file for exporting." << endl;
        return;
    }

    outFile << "Student Name\tFinal Grade" << endl;

    for (const Student& student : students) {
        outFile << student.name << "\t" << student.finalGrade << endl;
    }

    cout << "Exported student grades to " << filename << endl;
    outFile.close();
}

int main() {
    vector<Student> students;

    while (true) {
        cout << "Options:\n";
        cout << "1. Add Student\n";
        cout << "2. Display Statistics\n";
        cout << "3. Export Report\n";
        cout << "4. Exit\n";
        cout << "Enter your choice: ";

        int choice;
        cin >> choice;

        switch (choice) {
            case 1:
                addStudent(students);
                break;
            case 2:
                displayStatistics(students);
                break;
            case 3: {
                string filename;
                cout << "Enter the filename to export: ";
                cin >> filename;
                exportReport(students, filename);
                break;
            }
            case 4:
                return 0;  // Exit the program
            default:
                cout << "Invalid input. Please enter a valid choice." << endl;
                cin.clear();
                cin.ignore(numeric_limits<streamsize>::max(), '\n');
        }
    }

    return 0;
}
