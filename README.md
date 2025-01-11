# Shell-sort-and-my-own-sorting-algorithms


/*
Sandra Futwi
Sep/15/2024
Program 1, Fundamentals of Algorithms
This program will sort array of integers using differents gaps 
*/

public class ShellSort {

    public static void ShellSort(MyObj[] arr, int code) {
        // The code restricts on the given on h lists 
        if (code < 0 || code > 3) {
            System.err.println("Error, Must be 0, 1, 2, or 3.");
            System.exit(1);
        }

        // Creating hlist 
        int n = arr.length;
        int[] hlist = createHlist(n, code);
        //Insertion sort if case 0
        for (int h : hlist) {
            for (int i = h; i < n; i++) {
                MyObj temp = arr[i];
                int j = i;
                // descending order
                while (j >= h && !temp.lessThan(arr[j - h])) { 
                    arr[j] = arr[j - h];  
                    j -= h;
                }
                arr[j] = temp;
            }
        }
    }

    // Hlist based on the code
    private static int[] createHlist(int n, int code) {
        switch (code) {
            case 0:
                return new int[]{1}; // Insertion sort
            case 1:
                return generateHlistForCode1(n);
            case 2:
                return generateHlistForCode2(n);
            case 3:
                return generateHlistForCode3(n);
            default:
                return new int[]{1}; // Fallback
        }
    }

    // Code 1: [k^2, (k-1)^2, ..., 4, 1]
    private static int[] generateHlistForCode1(int n) {
        int k = 1;
        while (k * k < n) {
            k++;
        }
        int[] hlist = new int[k];
        for (int i = 0; i < k; i++) {
            hlist[i] = (k - i) * (k - i);
        }
        return hlist;
    }

    // Code 2: [2k-1, 2(k-1)-1, ..., 3, 1]
    private static int[] generateHlistForCode2(int n) {
        int k = 1;
        while (2 * k - 1 < n) {
            k++;
        }
        int[] hlist = new int[k];
        for (int i = 0; i < k; i++) {
            hlist[i] = 2 * (k - i) - 1;
        }
        return hlist;
    }

    // Code 3: [(3k-1)/2, (3(k-1)-1)/2, ..., 4, 1]
    private static int[] generateHlistForCode3(int n) {
        int k = 1;
        while ((3 * k - 1) / 2 < n) {
            k++;
        }
        int[] hlist = new int[k];
        for (int i = 0; i < k; i++) {
            hlist[i] = (3 * (k - i) - 1) / 2;
        }
        return hlist;
    }
}

import java.util.Scanner;
import java.util.Random;

public class MyObj {

	//Static compareCount:
	static int compareCount = 0;
	int a[] = new int[3];
	static Random r = new Random(System.currentTimeMillis());

//: create a MyObj object with the array value x, y, z respectively
	public MyObj(int x, int y, int z) {
		a[0] = x;
		a[1] = y;
		a[2] = z;
	}
// an array of	Int a[] : an array of 3 integers
	public MyObj() {
		//Create a MyObj object, with the values of the array being random numbers between 0 and 1000
		a[0] = r.nextInt(1000);
		a[1] = r.nextInt(1000);
		a[2] = r.nextInt(1000);
	}

//update the value of the array of the object to x, y, z respectively
	public void Update(int x, int y, int z) {
		a[0] = x;
		a[1] = y;
		a[2] = z;
	}

//return true if and only if the object is less than x.
//(See the code for the current definition of less than).
//Also increment compareCount by 1
	public boolean lessThan(MyObj x) {

		if (a[0] < x.a[0])
			return true;
		if ((a[0] == x.a[0]) && (a[1] < x.a[1]))
			return true;
		if ((a[0] == x.a[0]) && (a[1] == x.a[1]) && (a[2] < x.a[2]))
			return true;
		compareCount++;
		return false;
	}

	public void reset() {
		compareCount = 0;
	}
//return the current value of compareCount o Int reset(): set compareCount to 0
	public int getCount() {
		return compareCount;
	}

//print the object to the standard output
	public void print() {
		System.out.print("(" + a[0] + " " + a[1] + " " + a[2] + ")");


	}
}

import java.util.Scanner;

public class Prog1Test {
    
    public static void insertionSort(MyObj[] arr) {
        // Traverse through 1 to arr.length
        for (int i = 1; i < arr.length; i++) {
            MyObj key = arr[i];
            // Move elements of arr[0..i-1], that are greater than key, to one position ahead of their current position
            int j = i - 1;
            while (j >= 0 && arr[j].lessThan(key)) {
                arr[j + 1] = arr[j];
                j = j - 1;
            }
            arr[j + 1] = key;
        }
    }
    
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
   	MyObj a = new MyObj(1, 2, 3);
   	MyObj b = new MyObj(2, 2, 3);
 
	System.out.println(a.lessThan(b));
	System.out.println(b.lessThan(a));
	a.print();
	b.print();

	MyObj c[] = new MyObj[3];
	for (int i = 0; i < 3; i++) {
		c[i] = new MyObj();
		c[i].print();
	}

	MyObj temp = c[0];
	c[0] = c[1];
	c[1] = temp;
	System.out.println(" ");
	for (int i = 0; i < 3; i++) {
		c[i].print();
	}
	System.out.println(" ");
	ShellSort.ShellSort(c, 1);
	for (int i = 0; i < 3; i++) {
		c[i].print();
	}

    }
}

