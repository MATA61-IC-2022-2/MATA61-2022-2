# Programas em C-

## GCD

```
// A program to perform Euclid's
// Algorithm to compute gcd.

int gcd (int u, int v) {
    if (v == 0) 
       return u ;
    else 
       return gcd(v,u-u/v*v); // u-u/v*v == u mod v
}

void main(void) {
    int x; int y;
    x = input(); y = input();
    println(gcd(x,y));
}
```

## Selection Sort

```
// A program to perform selection sort on a 10-element array 

int x[10];

int minloc(int a[], int low, int high) {
    int i; int x; int k;
    k = low;
    x = a[low];
    i = low + 1;
    while (i < high) do {
        if (a[i] < x) {
            x = a[i];
            k = i;
        }
        i = i + 1;
    }
    return k;
}
void sort(int a[], int low, int high) {
    int i; int k;
    i = low;
    while (i < high - 1) do {
        int t;
        k = minloc(a, i, high);
        t = a[k];
        a[k] = a[i];
        a[i] = t;
        i = i + 1;
    }
}
void main(void) {
    int i;
    i = 0;
    while (i < 10) do {
        x[i] = input();
        i = i + 1;
    }
    sort(x, 0, 10);
    i = 0;
    while (i < 10) do {
        println(x[i]);
        i = i + 1;
    }
}
```
