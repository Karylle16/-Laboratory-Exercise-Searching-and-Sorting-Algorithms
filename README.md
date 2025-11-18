Activity 1 – Implementing Searching Algorithms
#include <iostream>
using namespace std;

// Linear Search
int linearSearch(int arr[], int n, int key) {
    for (int i = 0; i < n; i++)
        if (arr[i] == key) return i;
    return -1;
}

// Binary Search (Requires Sorted Array)
int binarySearch(int arr[], int n, int key) {
    int low = 0, high = n - 1;

    while (low <= high) {
        int mid = (low + high) / 2;

        if (arr[mid] == key)
            return mid;
        else if (arr[mid] < key)
            low = mid + 1;
        else
            high = mid - 1;
    }
    return -1;
}

// Interpolation Search (Works Best on Uniformly Distributed Data)
int interpolationSearch(int arr[], int n, int key) {
    int low = 0, high = n - 1;

    while (low <= high && key >= arr[low] && key <= arr[high]) {

        if (low == high) { 
            if (arr[low] == key) return low;
            return -1;
        }

        int pos = low + (((double)(high - low) /
                (arr[high] - arr[low])) * (key - arr[low]));

        if (arr[pos] == key)
            return pos;

        if (arr[pos] < key)
            low = pos + 1;
        else
            high = pos - 1;
    }

    return -1;
}

int main() {
    int arr[] = {12, 25, 37, 45, 56, 67, 72, 81, 90, 100};
    int n = 10, key, choice, result;

    cout << "Enter element to search: ";
    cin >> key;

    cout << "\nChoose Searching Algorithm:\n";
    cout << "[1] Linear Search\n";
    cout << "[2] Binary Search\n";
    cout << "[3] Interpolation Search\n";
    cout << "Choice: ";
    cin >> choice;

    switch (choice) {
        case 1:
            result = linearSearch(arr, n, key);
            break;
        case 2:
            result = binarySearch(arr, n, key);
            break;
        case 3:
            result = interpolationSearch(arr, n, key);
            break;
        default:
            cout << "Invalid choice!" << endl;
            return 0;
    }

    if (result != -1)
        cout << "Element found at index: " << result << endl;
    else
        cout << "Element not found!" << endl;

    return 0;
}

Activity 2 – Implementing Sorting Algorithms
