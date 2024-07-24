Program to find all pairs on integer array
Here, on this page, we will discuss the program to find all pairs whose sum is equal to a given number in Java . We are given an array and a value sum and we need to return the count of all the pairs whose sum is equal to a given value of the sum.

Example :

Input :

arr[] = {1, 5, 7, -1}   sum = 6

Output :

2 ( Pairs with sum 6 are (1, 5) and (7, -1) )
Program to find all pairs on integer array whose sum is equal to given number
Method 1 (Brute Force Approach)
 A simple solution is to traverse each element and check if there’s another number in the array which can be added to it to give sum. 

Program to find all pairs on integer array whose sum is equal to given number
Program to find all pairs on integer array
Run
public
class Main {
    public
    static void main(String args[]) {
        int[] arr = {1, 5, 7, -1, 5};
        int sum = 6;
        getPairsCount(arr, sum);
    }
    // Prints number of pairs in arr[0..n-1] with sum equa
    // to 'sum'
    public
    static void getPairsCount(int[] arr, int sum) {
        int count = 0;  // Initialize result

        // Consider all possible pairs and check their sums
        for (int i = 0; i < arr.length; i++)
            for (int j = i + 1; j < arr.length; j++)
                if ((arr[i] + arr[j]) == sum) count++;
        System.out.printf("Count of pairs is %d", count);
    }
}
Count of pairs is 3
Time and Space Complexities
Time complexity : O(n^2) Space Complexity : O(1)
Related Pages
Given an array which consists of only 0, 1 and 2

Move all the negative elements to one side of the array

Find the Union and Intersection of the two sorted arrays

Find Largest sum contiguous Subarray

Minimize the maximum difference between heights 

Method 2 (Using Hash-Map)
Make a map to keep track of the frequency of each number in the array. (Only one traversal is required.)
In the following traversal, for each element, determine whether it can be combined with any other element (other than itself!) to produce the desired sum. Increase the counter as needed.
Because each pair is counted twice, we’d have twice the required value in the counter at the end of the second traversal. As a result, divide count by 2 and return.
Time and Space Complexities
Time complexity : O(n) Space Complexity : O(n)
Code in Java :
Run
import java.util.HashMap;
public class Main
{
    static int arr[] = new int[] { 1, 5, 7, -1, 5 };
 
    // Returns number of pairs in arr[0..n-1] with sum equal
    // to 'sum'
    static int getPairsCount(int n, int sum)
    {
        HashMap<Integer, Integer> hm = new HashMap<>();
 
        // Store counts of all elements in map hm
        for (int i = 0; i < n; i++) {
 
            // initializing value to 0, if key not found
            if (!hm.containsKey(arr[i]))
                hm.put(arr[i], 0);
 
            hm.put(arr[i], hm.get(arr[i]) + 1);
        }
        int twice_count = 0;
 
        // iterate through each element and increment the
        // count (Notice that every pair is counted twice)
        for (int i = 0; i < n; i++) {
            if (hm.get(sum - arr[i]) != null)
                twice_count += hm.get(sum - arr[i]);
 
            // if (arr[i], arr[i]) pair satisfies the
            // condition, then we need to ensure that the
            // count is decreased by one such that the
            // (arr[i], arr[i]) pair is not considered
            if (sum - arr[i] == arr[i])
                twice_count--;
        }
 
        // return the half of twice_count
        return twice_count / 2;
    }
 
    // Driver method to test the above function
    public static void main(String[] args)
    {
 
        int sum = 6;
        System.out.println(
            "Count of pairs is "
            + getPairsCount(arr.length, sum));
    }
}
Count of pairs is 3
