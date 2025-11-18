# Activity 1 – Implementing Searching Algorithms
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

# Activity 2 – Implementing Sorting Algorithms
#include <iostream>
using namespace std;

// ---------------------- Bubble Sort ----------------------
void bubbleSort(int arr[], int n) {
    for (int i = 0; i < n - 1; i++)
        for (int j = 0; j < n - i - 1; j++)
            if (arr[j] > arr[j + 1])
                swap(arr[j], arr[j + 1]);
}

// ---------------------- Insertion Sort ----------------------
void insertionSort(int arr[], int n) {
    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
    }
}

// ---------------------- Selection Sort ----------------------
void selectionSort(int arr[], int n) {
    for (int i = 0; i < n - 1; i++) {
        int minIndex = i;
        for (int j = i + 1; j < n; j++)
            if (arr[j] < arr[minIndex])
                minIndex = j;
        swap(arr[minIndex], arr[i]);
    }
}

// ---------------------- Merge Sort ----------------------
void merge(int arr[], int left, int mid, int right) {
    int n1 = mid - left + 1;
    int n2 = right - mid;

    int L[n1], R[n2];

    for (int i = 0; i < n1; i++) L[i] = arr[left + i];
    for (int i = 0; i < n2; i++) R[i] = arr[mid + 1 + i];

    int i = 0, j = 0, k = left;

    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) arr[k++] = L[i++];
        else arr[k++] = R[j++];
    }

    while (i < n1) arr[k++] = L[i++];
    while (j < n2) arr[k++] = R[j++];
}

void mergeSort(int arr[], int left, int right) {
    if (left < right) {
        int mid = (left + right) / 2;
        mergeSort(arr, left, mid);
        mergeSort(arr, mid + 1, right);
        merge(arr, left, mid, right);
    }
}

// ---------------------- Quick Sort ----------------------
int partitionQ(int arr[], int low, int high) {
    int pivot = arr[high];
    int i = low - 1;

    for (int j = low; j < high; j++) {
        if (arr[j] < pivot) {
            i++;
            swap(arr[i], arr[j]);
        }
    }
    swap(arr[i + 1], arr[high]);
    return i + 1;
}

void quickSort(int arr[], int low, int high) {
    if (low < high) {
        int pi = partitionQ(arr, low, high);
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

// ---------------------- Heap Sort ----------------------
void heapify(int arr[], int n, int i) {
    int largest = i;
    int left = 2 * i + 1;
    int right = 2 * i + 2;

    if (left < n && arr[left] > arr[largest]) largest = left;
    if (right < n && arr[right] > arr[largest]) largest = right;

    if (largest != i) {
        swap(arr[i], arr[largest]);
        heapify(arr, n, largest);
    }
}

void heapSort(int arr[], int n) {
    for (int i = n / 2 - 1; i >= 0; i--)
        heapify(arr, n, i);

    for (int i = n - 1; i >= 0; i--) {
        swap(arr[0], arr[i]);
        heapify(arr, i, 0);
    }
}

// ---------------------- Shell Sort ----------------------
void shellSort(int arr[], int n) {
    for (int gap = n / 2; gap > 0; gap /= 2) {
        for (int i = gap; i < n; i++) {
            int temp = arr[i];
            int j = i;
            while (j >= gap && arr[j - gap] > temp) {
                arr[j] = arr[j - gap];
                j -= gap;
            }
            arr[j] = temp;
        }
    }
}

// ---------------------- Helper: Print Array ----------------------
void printArray(int arr[], int n) {
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
    cout << endl;
}

// ---------------------- MAIN PROGRAM ----------------------
int main() {
    int n = 10, arr[10];
    cout << "Enter 10 integers:\n";
    for (int i = 0; i < n; i++) cin >> arr[i];

    cout << "\nChoose Sorting Algorithm:\n";
    cout << "[1] Bubble Sort\n";
    cout << "[2] Insertion Sort\n";
    cout << "[3] Selection Sort\n";
    cout << "[4] Merge Sort\n";
    cout << "[5] Quick Sort\n";
    cout << "[6] Heap Sort\n";
    cout << "[7] Shell Sort\n";

    int choice; 
    cin >> choice;

    switch (choice) {
        case 1: bubbleSort(arr, n); break;
        case 2: insertionSort(arr, n); break;
        case 3: selectionSort(arr, n); break;
        case 4: mergeSort(arr, 0, n - 1); break;
        case 5: quickSort(arr, 0, n - 1); break;
        case 6: heapSort(arr, n); break;
        case 7: shellSort(arr, n); break;
        default: 
            cout << "Invalid choice!";
            return 0;
    }

    cout << "\nSorted Array: ";
    printArray(arr, n);

    return 0;
}

