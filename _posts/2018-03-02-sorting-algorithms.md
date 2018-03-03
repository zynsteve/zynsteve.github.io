---
title: Sorting Algorithms
description: Comparsion and Java Implementation of various sorting algorithms.
categories:
- Algorithm
tags:
- Java
---


## Selection Sort
```java
public void selectionSort (int[] array) {
    int i, j, minValue, minIndex, temp = 0;
    for (i = 0; i < array.length; i++) {
        minValue = array[i];
        minIndex = i;
        for (j = i; j < array.length; j++) {
            if (array[j] < minValue) {
                minValue = array[j];
                minIndex = j;
            }
        }
        if (minValue < array[i]) {
            temp = array[i];
            array[i] = array[minIndex];
            array[minIndex] = temp;
        }
    }
}
```
Time complexity: $O(n^2)$

## Insertion Sort
```Java
public void insertionSort (int[] array) {
    int i, j, key, temp;
    for (i = 1; i < array.length; i++) {
        key = array[i];
        j = i - 1;
        while (j >= 0 && key < array[j]) {
            temp = array[j];
            array[j] = array[j + 1];
            array[j + 1] = temp;
            j--;
        }
    }
}
```
Time complexity: $O(n^2)$

## Bubble Sort
```Java
public void bubbleSort (int[] array) {
    int i, j, temp = 0;
    for (i = 0; i < array.length - 1; i++) {
        for (j = 0; j < array.length - 1 - i; j++) {
            if (array[j] > array[j + 1]) {
                temp = array[j];
                    array[j] = array[j + 1];
                    array[j + 1] = temp;
            }
        }
    }
}
```
Time complexity: $O(n^2)$

## Merge Sort
```Java
public void mergeSort(int[] array) {
    mergeSort(array, 0, array.length - 1);
}

public void mergeSort (int[] array, int lowIndex, int highIndex) {
    if (lowIndex == highIndex) return;
    else {
        int midIndex = (lowIndex + highIndex) / 2;
        mergeSort(array, lowIndex, midIndex);
        mergeSort(array, midIndex + 1, highIndex);
        merge(array, lowIndex, midIndex, highIndex);
    }
}

public void merge(int[] array, int lowIndex, int midIndex, int highIndex) {
    int[] left = new int[midIndex - lowIndex + 2];
    for (int i = lowIndex; i <= midIndex; i++) left[i - lowIndex] = array[i];
    left[midIndex - lowIndex + 1] = Integer.MAX_VALUE;

    int[] right = new int[highIndex - midIndex + 1];
    for (int i = midIndex + 1; i <= highIndex; i++) right[i - midIndex - 1] = array[i];
    right[highIndex - midIndex] = Integer.MAX_VALUE;

    int i = 0, j = 0;
    for (int k = lowIndex; k <= highIndex; k++) {
        if (left[i] <= right[j]) {
            array[k] = left[i];
            i++;
        } else {
            array[k] = right[j];
            j++;
        }
    }
}
```
Time complexity: $O(n\log n)$

## Quick Sort
```Java
public void quickSort(int[] array) {
    quickSort(array, 0, array.length-1);
}

private void quickSort(int[] array, int low, int high) {
    if (low < high + 1) {
    int p = partition(array, low, high);
    quickSort(array, low, p - 1);
    quickSort(array, p + 1, high);
    }
}

private void swap(int[] array, int index1, int index2) {
    int temp = array[index1];
    array[index1] = array[index2];
    array[index2] = temp;
}

private int getPivot(int low, int high) {
    Random rand = new Random();
    return rand.nextInt((high - low) + 1) + low;
}

private int partition(int[] array, int low, int high) {
    swap(array, low, getPivot(low, high));
    int border = low + 1;
    for (int i = border; i <= high; i++) {
        if (array[i] < array[low]) {
            swap(array, i, border++);
        }
    }
    swap(array, low, border - 1);
    return border - 1;
}
```
Time complexity: $O(n\log n)$
