### نوشته شده در نرم افزار obsidian با markdown
---

## سوال اول - بازی اعداد اول

```c
#include <stdio.h>

// Code by mhr85

void YES() {
    printf("YES\n");
}
void NO() {
    printf("NO\n");
}

int main() {

    int n;
    scanf("%d", &n);
    
    // Check if it is not 2 and divideable to 2 or it is 1 -> it is not prime
    if (n != 2 && n % 2 == 0 || n == 1)
    {
        NO();
        return 0;
    }
    
    // only divideable to odd numbers or not
    for(int i = 3; i < n; i += 2) {
        
        if (n % i == 0)
        {
            NO();
            return 0;
        }
        
    }
    
    YES();
    return 0;
    
}
```

ابتدا بررسی می کنیم که عدد بر دو بخش پذیر است یا نه (نباید خود ۲ یا ۱ باشد) در این صورت عدد اول نیست (۱ عدد اول نیست)
سپس بخش پذیری آن بر اعداد فرد کوچک تر از خودش را بررسی می کنیم.
اگر بر آنها هم بخش پذیر نبود عدد اول است

## سوال دوم - کامل بودن یا نبودن

```c
#include <stdio.h>   

// to check running time and printing the algorithm prograccing notes change it to 1
#define DEBUG 0

// Code by mhr85

void YES() {
    printf("YES\n");
}
void NO() {
    printf("NO\n");
}

int main() {

    int n;
    scanf("%d", &n);
    
    int sum = 0;
    
    for(int i = n-1; i > 0; i--) {
        
        if (n % i == 0)
        {
            
            sum += i;
            
        }
        
    }
    
    if (sum == n) {
        YES();
    } else {
        NO();
    }
    
    return 0;
    
}
```

متغیر sum شمارنده تعداد مقسوم علیه های کوچک تر از n است. عدد را بر همه اعداد بین ۱ تا عدد کوچک تر از خودش تقسیم می کنیم.
در نهایت اگر تعداد مقسوم علیه ها با خود آن برابر بود yes را چاپ می کنیم.

## سوال سوم - عدد خوب

```c
#include <stdio.h>   
#include <time.h>
#include <math.h>

// to check running time and printing the algorithm prograccing notes change it to 1
#define DEBUG 0

// Code by my friend :
// I get this code from my friend to check how much my code is effiecient.
// My code shows x70 faster result production in input = 150 !!


// MY FRIEND CODE TEST :
// ------------------------------------
// 150
// 749700
// Program running time ms : 753.389
// ------------------------------------



// MY CODE TEST :
// ------------------------------------
// 150
// 749700
// Program running time ms : 12.878
// ------------------------------------


// Start of code by my friend :
// ------------------------------------
// int tedad_Shomarande(int n)
// {
//     int i, counter = 0;
//     for (i = 1; i <= n; i++)
//     {
//         if (n % i == 0)
//         {
//             counter++;
//         }
//     }
//     return counter;
// }

// int program()
// {
//     int k, i = 1, good = 0;
//     scanf("%d", &k);

//     while (1)
//     {
//         if (tedad_Shomarande(good) >= k)
//         {
//             printf("%d", good);
//             return 0;
//         }

//         good += i;
//         i += 1;
//     }

// }
// ------------------------------------
// End of Code by my friend





// Code by mhr85 (mine)

// count how many time a prime repeats in a number
int countAPrime(int prime, int number) {
    
    number /= prime;
    int count = 1;
    
    while (number > 1 && number % prime == 0)
    {
        number /= prime;
        count++;
    }

    return count;
    
}

// 0 if it is prime and number > 0 if we found a shomarande and -1 if number is 1
int isPrime(int n) {

    // checking 2
    if (n != 2 && n % 2 == 0)
    {
        return 2;
    }
    
    // checking 1
    if (n == 1) return -1;

    // checking odd numbers
    for(int i = 3; i <= sqrt(n); i += 2) {
        
        if (n % i == 0)
        {
            // returns a prime number that the n is dividable with it. it is prime because it starts from lower numbers;
            return i;
        }
        
    }
    
    return 0;
    
}

// counts how many divisors the number n has
int countDivisors(int n) {
    int tempN = n;
    if (tempN == 1) {
        return 1;
    }

    int divisorCount = 1;

    while (1)
    {
        int shomarande = isPrime(tempN);

        // if (DEBUG)
        // {
        //     printf("n: %d, shomarande : %d, primeCount : %d\n", n, shomarande, primeCount);
        // }
        
        // numbers is 1, no any another divisors
        if (shomarande == -1)
        {
            break;
        } else if (shomarande > 0)
        {
            int howMuchWeHaveIt = countAPrime(shomarande, tempN);
            divisorCount *= howMuchWeHaveIt + 1;
            tempN /= pow(shomarande, howMuchWeHaveIt);
        } else if (shomarande == 0)
        {
            tempN = 1;
            divisorCount *= 2;
        }
    }
    if (DEBUG)
    {
        printf("n: %d, primeCount : %d\n", n, divisorCount);
    }
    return divisorCount;
}

int program() {

    int inp;
    scanf("%d", &inp);

    int n = 1;
    while (1)
    {
        // num is an adad khoob
        int num = n * (n+1) / 2;        
        int divisorsCount = countDivisors(num);
        
        if (DEBUG) printf("n: %d, num: %d, c:%d\n", n, num, divisorsCount);

        if (divisorsCount >= inp)
        {            
            printf("%d\n", num);
            break;
        }
        n += 1;

    }

    return 0;

}


// if DEBUG is 1 it will calculate run time, elsewhere it run program without any time tracking
int main() {
    
    if (DEBUG) {

        clock_t c_start = clock();
        int result = program();
        clock_t c_end = clock();

        float p_time = (c_end - c_start)*1000 / (float) CLOCKS_PER_SEC;
        printf("Program running time ms : %.3f\n", p_time);

        return result;

    } else {

        return program();

    }
    
}
```

دیفاین دیباگ برای بررسی زمان اجرای نرم افزار و اجرای پرینت های مربوط به دیباگ است. اگر مقدار آن ۱ باشد.
در تابع main ما تابع program را اجرا می کنیم ( اگر دیباگ فعال باشد زمان اجرای آن را هم اندازه می گیریم )
من الگوریتمی نوشتم که از کد دوستم خیلی سریع تر اجرا میشد و کد دوستم که ساده ترین راه حل سوال است را قرار دادم. در ورودی ۱۵۰ کد من ۷۰ برابر سریع تر عمل کرد. برای بررسی سرعت کد از time.h و تابع clock موجود در آن استفاده کردم.
تابع isPrime را به گونه ای نوشتم که اگر عدد اول باشد ۰ را برگرداند، اگر ۱ باشد -۱ را بر می گرداند و اگر مرکب باشد یک شمارنده اول از آنرا.
برای پیدا کردن تعداد مقسوم علیه ها از تابع isPrime در تابع countDivisors استفاده کردم.
در حلقه وایل موجود در تابع countDivisors خروجی تابع isPrime برای عدد داده شده بررسی می شود. یک متغیر شمارنده مقسوم علیه با مقدار اولیه ۱ در بیرون حلقه تعریف شده که این مقدار برای عدد ۱ می باشد.
ساز و کار به این صورت است که اگر مقسوم علیه اولی برای ورودی مان پیدا کنیم شمارنده مقسوم علیه ها را ضرب در (تعداد آن عامل اول + ۱) می کنیم. زیرا هر عدد اولی به صورت p به توان n که در عددی وجود داشته باشه n + 1 حالت در روش ساخت همه مقسوم علیه ها به حالات اضافه می کند. پس از اضافه کردن به شمارنده مقسوم علیه ها عدد را تقسیم بر p به توان n می کنیم تا عامل اول مورد نظر از عدد خارج شود و به عوامل دیگر بپردازیم.
هر گاه به عددی رسیدیم که خود آن عدد اول بود یعنی از آن عامل اول فقط یکی در آن عدد اولیه ورودی تابع وجود دارد. پس ۲ حالت بودن و نبودن دارد پس شمارنده مقسوم علیه ها را ضرب در ۲ می کنیم و عدد را تقسیم بر ان عامل اول تا عدد در نهایت خود ۱ شود و از حلقه خارج شویم.

در تابع اصلی program، اعداد خوب را یکی یکی ایجاد می کنیم ( متغیر num ) و بررسی می کنیم که آیا تعداد شمارنده های آنها از خودشان بیشتر مساوی است یا نه و اگر بود چاپ می کنیم و خارج می شویم.

## سوال چهارم - Gravity Falls

```c
#include <stdio.h>   
#include <math.h>

// Code by mhr85

float logWithBase(float base, float num) {
    if (base == 0 || num == 0 || base == 1)
    {
        return -1;
    }
    
    return log10f(num) / log10f(base);
}

int main() {

    int n, b1, b2;
    scanf("%d %d %d", &n, &b1, &b2);
    
    // START: convert n to decimal from base b1
    
    int nDecimal = 0;
    // iteration in the digits from right
    for (int i = 1; i <= log10f(n) + 1; i++) {
        int digitI = (n / (int)powf(10, i - 1)) % 10;
        nDecimal += digitI * pow(b1, i - 1);
    }
    
    // END: convert n to decimal from base b1
    
    // START: convert nDecimal to base b2
    
    // count the digits of the b2 number
    
    int nDecimalTemp = nDecimal;
    int digitCount = logWithBase(b2, nDecimal) + 1;
    if (digitCount < 1)
    {
        digitCount = 1;
    }
    
    // we are making digits for base b2 from left
    for (int i = 1; i <= digitCount; i++)
    {
        int power = digitCount - i;
        int checkingNumber = powf(b2, power);
        
        // printf("Checking number : %d, result: ", checkingNumber);
        if (nDecimalTemp >= checkingNumber)
        {
            // for example 3 of 4^3 if b2 is 4
            int howManyFromCheckingNumToSubtract = nDecimalTemp / checkingNumber;
            
            // add it to representation
            printf("%d", howManyFromCheckingNumToSubtract);
            
            // subtract the number we can subtract from nDecimalTemp
            nDecimalTemp -= howManyFromCheckingNumToSubtract * checkingNumber;
        } else {
            printf("0");
        }
        
        // printf("num : %d, decimal representation: %d\n", i, decimalRepresentationOfBaseB2);
    }
    // END: convert nDecimal to base b2
    printf("\n");
    
    // printf("%d\n", decimalRepresentationOfBaseB2);
    
}
```

حل این سوال را به گونه ای نوشتم که هر عددی از هر مبنایی بین 2 تا 10 را به یکدیگر تبدیل کند.
تابل لوگاریتم بر مبنای دلخواه را بر اساس فرمول ریاضی زیر نوشتم : $$log_a b = \frac{log_{10} b}{log_{10} a}$$
در این سوال من همه اعداد ورودی بر هر مبنایی را به دسیمال تبدیل کرده سپس به مبنای خروجی تبدیل می کنم.
ورودی در ظاهر عددی از مبنای 10 است پس باید هر رقم را با کد زیر بدست آورد(حتی اعداد در مبنای ۶  هم به صورت یک عدد دسیمال وارد سیستم می شوند ولی واقعا دسیمال نیستند)
```c
int digitI = (n / (int)powf(10, i - 1)) % 10;
```
سپس هر رقم را ضرب در مبنای مورد نظر به توان i - 1 می کنیم. دقت کنید که در فور نوشته شده ما log10(n) + 1 که ورودی لوگاریتم همان عدد به ظاهر دسیمال است ، رقم در مبنای b1 داریم. 
متغیر i در فور نشان دهنده رقم i ام از سمت راست است. رقم دوم نشان دهنده تعداد b1^1 خواهد بود رقم سوم b1^2 و ...
با این روش ورودی را از هر مبنایی دسیمال می کنیم.
سپس باید عدد دسیمال را به مبنای مقصد ببریم.
این کار را از توان بزرگ تر یعنی سمت چپ شروع می کنیم. برای مشخص کردن تعداد ارقام عدد در مبنای b2 از لگوریتم عدد دسیمال بر مبنای b2 استفاده شده. در نگاه اول نباید آنرا به علاوه یک کنیم ولی وقتی دقت کنید متوجه می شوید که در آخرین رقم b2^0 را داریم.
سپس از سمت چپ بررسی می کنیم که مثلا برای عددی در مبنای ۴ با ۶ رقم در ابتدا چند تا 4 به توان 5 می توان از آن کم کرد و آنرا چاپ می کنیم. سپس چند تا ۴ به توان ۴ تا چند تا ۴ به توان ۰ که همان ۱ است. و هر بار مقدار مورد نظر را از عدد کم می کنیم تا در نهایت عدد دسیمالمان صفر شده و عدد ایجاد شده در مبنای b2 به طور کامل چاپ شود. دقت کنید که ما هر رقم را از سمت چپ تولید و چاپ می کنیم و نیازی به ذخیره و چاپ یکباره آن نیست.

## سوال پنجم - چاپ لوزی

```c
#include <stdio.h>   
#include <math.h>
#include <stdlib.h>

// Code by mhr85

int main() {

    // index map ji -> first j and then i
    
    /* 
    00 10 20 30 ..
    01 11 21 31 ..
    02 12 22 32 ..
    03 13 23 33 ..
    .. .. .. .. ..
    */
    
    int n;
    scanf("%d", &n);
    
    for (int i = 0; i < 2*n + 1; i++) {
    
        // first point to print j index
        int i_f = abs(n - i);
        // last point to print j index
        int i_l = 2*n - i_f;
        
        for (int j = 0; j < 2*n + 1; j++)
        {
        
            // check if we need to print point or not
            if (j < i_f || j > i_l)
            {
                printf(" ");
            } else {
                printf("*");
            }
            
        }
        printf("\n");
        
    }
    
}
```

به این کد نگاه نکنید! له شدم تا وقتی به این رسیدم چند فرمول نوشتم و پاک کردم تا این شد. در این کد از آرایه استفاده نشده ولی برای مدل سازی فرض کنید ما یک جدول مربعی به ضلع 2n+1 در صفحه چاپ داریم.

همان طور که در کامنت می بینید یک ایندکس مپ به صورت زیر فرض کنید توجه کنید در این سوال بر عکس معمول از i به عنوان شماره ردیف و از j به عنوان شماره ستون استفاده شده
سپس باید در دو فور تو در تو تمام عناصر را بررسی کنیم و ببینیم که یک اسپیس چاپ شود یا ستاره. i_f اندیس اولین نقطه در یک ردیف برای چاپ ستاره را مشخص می کند که وابسته به i یعنی شماره ردیف است. اگر دقت کنید برای یک لوزی به قطر ۵ یعنی n برابر ۲ داریم :
```
 01234
0  *  
1 *** 
2*****
3 ***
4  * 
```

و اندیس اولین نقطه برای چاپ در ردیف اول i = 0 همان ۲ یا n است
در ردیف دوم i = 1 همان ۱ است
در ردیف سوم i = n همان صفر است.
پس i_f تابع قدر مطلقی مشخص شده در کد می باشد.
از روی i_f متغیر i_l یعنی آخرین اندیس چاپ ستاره را پیدا می کنیم.
سپس در شماره ستون ها j پیمایش کرده و طبق i_f و i_l مشخص می کنیم که کجا ستاره چاپ شود و کجا نه.

## سوال ششم - compute

```c
#include <stdio.h>   

// Code by mhr85

int myAbs(int n) {
    return n >=0 ? n : -n;
}

int absMinusXCalculator(int c, int x) {
    // decreasing c to 0
    
    if (c == 0) {
        // we 'really' use x just in the last turn of recursive chain
        return myAbs(x);
    } else {
        return myAbs(absMinusXCalculator(c - 1, x) - c);
        //           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
        //           calling itself with a lower c
    }
    
}

int f(int x) {
    return absMinusXCalculator(10, x);
}

int main() {

    int sum = 0;
    //   sum of f(1) to f(55)
    for (int i = 1; i <= 55; i++)
    {
        sum += f(i);
    }
    
    printf("%d\n", sum);
    
}
```

در این مورد خاص تابع f از 10 شروع کرده که ما آنرا c نامیده ایم. بقیه توضیحات در کامنت ها کاملا واضح شرح داده شده و نیازی به توضیح ندارد. 

## سوال هفتم - تابع محصولی

```c
#include <stdio.h>   

// Code by mhr85

int main() {

    int a, b, c, alpha, beta;
    scanf("%d %d %d", &a, &b, &c);
    scanf("%d %d", &alpha, &beta);
    
    for (int i = alpha; i <= beta; i++)
    {
        printf("%d", a*i*i + b*i + c); // a*(i^2) + bi + c
        if (i != beta)
        {
            printf(" ");
        }
    }
    
    printf("\n");
    
}
```

بدون شرح! آخه ازین ساده تر دیگه؟

## سوال هشتم - زیر مجموعه های دوتایی

```c
#include <stdio.h>   
#include <limits.h>
#include <stdlib.h>

// Code by mhr85

int main() {
    
    int n;
    scanf("%d", &n);
    
    // array with size n
    int a[n];
    
    for (int i = 0; i < n; i++)
    {
        scanf("%d", &a[i]); 
        // a is the pointer for first element of array so we can use this instead:
        // scanf("%d", a + i);
    }
    
    int min = abs(a[0]-a[1]), add = a[0]+a[1];
    
    if(min != 0)
        for (int i = 0; i < n; i++)
        {
            for (int j = n - 1; j > i; j--)
            {
                int diff = abs(a[i] - a[j]);
                int add_new = a[i] + a[j];
                if (diff <= min && (diff < min || add_new > add))
                {
                    min = diff;
                    add = add_new;
                    if(min == 0) {
                        break;
                    }
                }
            }
            if(min == 0) {
                break;
            }
        }
    
    printf("%d\n", add);
    
}
```

یک آرایه تعریف و تمام ورودی ها را در آن ذخیره می کنیم. سپس مشخص می کنیم و سپس مقدار اولیه min که نشان دهنده اختلاف است را اختلاف دو مورد اول و جمع را جمع دو مورد اول قرار می دهیم. سپس می خواهیم در یک حلقه به طور مکرر اختلاف تمام جملات را با یکدیگر بررسی کنیم و اگر کمتر بود min و add را بروز رسانی کنیم.
از ساختار حلقه تو در تو استفاده می کنیم به طوری که i , j های بصورت زیر داشته باشیم تا هر جفت دقیقا یک بار با هم بررسی شوند:

به فرض برای n = 5 :
```
i j
---
0 4
0 3
0 2
0 1
1 4
1 3
1 2
2 4
2 3
3 4
```

حال در این حلقه یک diff جدید پیدا می کنیم . یک if نوشته ایم که بررسی می کند:

اگر اختلاف موارد جدید diff از کمترین اختلاف موارد قبلی min کمتر مساوی بود:
	اگر اختلاف موارد جدید دقیقا کمتر از کمترین اختلاف موارد قبلی بود
	یا جمع آنها بیشتر از جمع موارد با کمترین اختلاف قبلی بود
		آنگاه کمترین اختلاف موارد قبلی را برابر با اختلاف موارد جدید کن و جمع موارد با کمترین اختلاف قبلی را برابر با جمع موارد جدید کن

دقت کنید که اگر اختلاف آنها به صفر رسیده باشد کمترین اختلاف است و باید از هر دو حلقه خارج شویم پس در دو if بررسی کرده ایم و در این صورت با خروج از حلقه اول و سپس حلقه دوم برنامه تمام می شود

## سوال نهم - مسیر مارپیچی

```c
#include <stdio.h>   
#include <time.h>


#define DEBUG 0

// Code by mhr85

int program() {

    int n;
    scanf("%d", &n);
    
    if (n == 1)
    {
        printf("%3d\n", 1); // makes problem with quera code corrector, but in the example output you use 3 character space container.
        return 0;
    }
    
    
    int m[n][n];
    
    // next number to print
    int num = 1;
    
    // in each loop we make one squarel. in loop one we create
    // n*n squrel and next time we create we create (n-1)*(n-1) until 2*2 or 3*3 squrel
    for (int loopI = 0; loopI < (n / 2); loopI++)
    {
        int i,j;
        
        int currentFillingN = n - 2 * loopI;
        
        // to print from first itom to n - 1 item in horizental
        int lastI = n - loopI - 2;
        j = loopI;
        for (i = loopI; i <= lastI; i++)
        {
            m[i][j] = num;
            if(DEBUG) printf("i : %d, for : 1 : setting m[%d][%d] to %d\n",loopI, i, j, num);
            num += 1;
        }
        
        int lastJ = n - loopI - 2;
        i = n - loopI - 1;
        for (j = loopI; j <= lastJ; j++)
        {
            m[i][j] = num;
            if(DEBUG) printf("i : %d, for : 2 : setting m[%d][%d] to %d\n",loopI, i, j, num);
            num += 1;
        }
        
        int firstI = n - loopI - 1;
        j = n - loopI - 1;
        for (i = firstI; i > loopI; i--)
        {
            m[i][j] = num;
            if(DEBUG) printf("i : %d, for : 3 : setting m[%d][%d] to %d\n",loopI, i, j, num);
            num += 1;
        }
        
        int firstJ = n - loopI - 1;
        i = loopI;
        for (j = firstI; j > loopI; j--)
        {
            m[i][j] = num;
            if(DEBUG) printf("i : %d, for : 4 : setting m[%d][%d] to %d\n",loopI, i, j, num);
            num += 1;
        }
        
        // make center item in the last loop for odd numbers
        if (n % 2 == 1 && currentFillingN == 3)
        {
            m[loopI+1][loopI+1] = num;
        }
        
    }
    
    // PRINTING RESULT
    for (int j = 0; j < n; j++)
    {
        for (int i = 0; i < n; i++)
        {
            // print it within a 3 character space container
            printf("%3d", m[i][j]); // makes problem with quera code corrector, but in the example output you use 3 character space container.
            if (i != n - 1)
            {
                // make an space between numbers
                printf(" ");
            }
        }
        printf("\n");
    }
    
    return 0;
    
}

int main() {
    
    if (DEBUG) {

        clock_t c_start = clock();
        int result = program();
        clock_t c_end = clock();

        float p_time = (c_end - c_start)*1000 / (float) CLOCKS_PER_SEC;
        printf("\nProgram running time ms : %.3f\n", p_time);

        return result;

    } else {

        return program();

    }
    
}
```

وای کی حوصله داره توضیح بده! ۴۰ دقه وقت گرفت یه سره دیباگ و ... چک و آزمایش خطا

ولی مث اینکه مجبوریم:

یه فور اصلی داریم میاد مربع مربع میکنه ناحیه رو و روی قطر مربعا حرکت می کنه
با مثال توضیح میدیم:
```
  1   2   3   4
 12  13  14   5
 11  16  15   6
 10   9   8   7
```

ما میایم اولین بار مربعی به شکل
```none
  1   2   3   4
 12           5
 11           6
 10   9   8   7
```
رو بررسی می کنیم

بعد مربعی به شکل 
```none

     13  14    
     16  15    
       
```

اینکارو تو فور اولی انجام دادیم

متغیر currentFillingN مشخص می کنه مربعی که الان داریم بررسی می کنیم چند در چنده یا همون طول ضلع مربی که الان داریم رو قطرش حرکت می کنیمو میده.

#### حالا تو حلقه اصلیمون ۴ تا حلقه دیگه داریم که برای مثالمون مرحله به مرحله کارای زیرو انجام میدن. فرض کنید مربع اولو میریم:

```none
  1   2   3   4
 12           5
 11           6
 10   9   8   7
```

حلقه اول :: حرکت افقی به سمت راست
```none
  1   2   3   *
  *           *
  *           *
  *   *   *   *
```

حلقه دوم :: حرکت عمودی به پایین
```none
  *   *   *   4
  *           5
  *           6
  *   *   *   *
```

حلقه سوم :: حرکت افقی به سمت چپ
```none
  *   *   *   *
  *           *
  *           *
  *   9   8   7
```

حلقه چهارم :: حرکت عمودی رو به بالا
```none
  *   *   *   *
 12           *
 11           *
 10   *   *   *
```

همه این عملیات ها برای یک مربع ۴ در ۴ انجام می شود و سپس برای مربع ۲ در ۲ با این تفاوت که برای مربع بعدی از ۱۳ شروع می کنیم.

### بررسی هر حلقه:
در حلقه اول میایم رو i ها پیمایش می کنیم و زیادش می کنیم تا به اندیس یکی به آخر مربع در حال بررسی توی ردیف افقیمون برسیم. اینکه تو مربع فعلی مورد بررسی ، کدوم اندیس اندیس یکی به آخره رو از روی loopI مشخص می کنیم. دقت کنید اینجا داریم روی یک j یا یک شماره ردیف ثابت حرکت می کنیم. از i = 0 یعنی چپ ترین آیتم شروع کردیم.

در حلقه دوم میایم رو j ها پیمایش می کنیم و زیادش می کنیم تا به اندیس یکی به آخر مربع در حال بررسی توی ستون عمودیمون برسیم. اینکه تو مربع فعلی مورد بررسی ، کدوم اندیس اندیس یکی به آخره رو از روی loopI مشخص می کنیم. دقت کنید اینجا داریم روی یک i یا یک شماره ستون ثابت حرکت می کنیم. از j = 0 یعنی بالا ترین آیتم شروع کردیم.

در حلقه سوم میایم رو i ها پیمایش می کنیم و کمش می کنیم تا به اندیس یکی قبل از اولین اندیس مربع در حال بررسی توی ردیف افیقیمون برسیم. باید طوری شروع کنیم که انگار از اندیس آخر ردیف افقیمون توی مربع مورد بررسی شروع کردیم. دقت کنید اینجا داریم روی یک j یا یک شماره ردیف ثابت حرکت می کنیم. از i = اندیس آخرین ستون در مربع مورد بررسی یعنی راست ترین آیتم شروع کردیم.

در حلقه چهارم میایم رو j ها پیمایش می کنیم و کمش می کنیم تا به اندیس یکی قبل از اولین اندیس مربع در حال بررسی توی ستون عمودیمون برسیم. باید طوری شروع کنیم که انگار از اندیس آخر ستون عمودیمون توی مربع مورد بررسی شروع کردیم. دقت کنید اینجا داریم روی یک i یا یک شماره ستون ثابت حرکت می کنیم. از j = اندیس آخرین ردیف در مربع مورد بررسی یعنی پایین ترین آیتم شروع کردیم.

#### دقت کنید که آخرین چرخشی که در فور اصلی انجام میدیم و آخرین مربعی که بررسی می کنیم بسته به اینکه n زوج باشه یا فرد 2 یا 3 خواهد بود. اگه n فرد باشه باید برای نقطه وسطی هم فکری بکنیم که در ایف آخر اینکارو کردیم 

## سوال دهم - رمزگشایی کد باینری

```c
#include <stdio.h>

// Code by mhr85

int main()
{

    int c = 0;

    int wFlag = 1;
    while (wFlag)
    {
        const int in = getchar();
        switch (in)
        {
        case '0':
            if (c > 0) printf("%d\n", c);
            c = 0;
            break;
        case EOF:
        case '\n':
            wFlag = 0;
            if (c > 0) printf("%d\n", c);
            break;
        default:
            c += 1;
            break;
        }
    }

    return 0;

}
```

متغیر c برای شمارش تعداد ۱ هاست. و از wFlag برای خروج از وایل استفاده شده چون بریک در سوییچ برای خارج شدن از وایل کاربردی نیست.
دقت کنید که ما در سوییچ کیسمون از case 1: استفاده نکردیم و کار اون رو به default سپردیم. یعنی هر کاراکتری جز صفر رو می شمریم.

## سوال یازدهم - سامان و پنج آتشین

```c
#include <stdio.h>   

// Code by mhr85

unsigned long long int F(int n) {
    
    // all steps done
    if (n == 0) {
        return 1;
    }

    // if we can step with a certain number we do it and calculate another steps situations,
    // otherwise we will set step situations number for the certain number to 0.
    // with 1 step :
    unsigned long long int situations1 = (n >= 1) ? F(n - 1) : 0;
    
    // with 2 step : 
    unsigned long long int situations2 = (n >= 2) ? F(n - 2) : 0;
    
    // with 3 step : 
    unsigned long long int situations3 = (n >= 3) ? F(n - 3) : 0;

    return situations1 + situations2 + situations3;

}

// NOT RECURSIVE -------------------------------------------------

// unsigned long long int factorial(unsigned long long int n) {
//     if (n == 1 || n == 0)
//     {
//         return 1;
//     }
    
//     return n * factorial(n-1);
// }


// unsigned long long int F(int n) {

//     unsigned const int bMax = n / 2;
//     unsigned const int cMax = n / 3;

//     unsigned long long int allSituatiionsCount = 0;

//     for (unsigned int c = 0; c <= cMax; c++)
//     {
        
//         for (unsigned int b = 0; b <= bMax; b++)
//         {

//             if (3*c + 2*b > n)
//             {
//                 break;
//             }

//             // we have b and c so we have a from equation
//             int a = n - 3*c - 2*b;

//             if(DEBUG) printf("a, b, c :: %d, 2* %d, 3* %d\n", a, b, c);

//             // jaaygasht baa azaye tekraree
//             unsigned long long const int newSituations = (factorial(a + b + c) / (factorial(a) * factorial(b) * factorial(c)));

//             if (newSituations > ULLONG_MAX - allSituatiionsCount)
//             {
//                 printf("OVERFLOW\n");
//                 return 0;
//             }
            
//             allSituatiionsCount += newSituations;

//         }
        
//     }

//     return allSituatiionsCount;

// }

// -------------------------------------------------------------


int main() {

    int n;
    scanf("%d", &n);

    printf("%lld\n", F(n));

    return 0;

}
```

مدل غیر بازگشتی این سوال رو از ایده دوستم نوشتم که داشت کد میزد کدش رو دیدم. اون موقع سوالو نخونده بودم و اصلا حواسم نبود که باید بازگشتی باشه و کد رو از رو اون ایده زدم. بعد که خواستم بفرستمش دیدم و به صورت بازگشتی زدمش. وقتی زدم کیف کردم حسابی چون دیدم خیلی ساده تر میشه.

کاری که ما می کنیم مث کشیدن یه درخته مثلا برای n = 5

```python
5
├── 4
│   ├── 3
│   │   ├── 2
│   │   │   ├── 1
│   │   │   │   └── 0
│   │   │   └── 0
│   │   ├── 1
│   │   │   └── 0
│   │   └── 0
│   ├── 2
│   │   ├── 1
│   │   │   └── 0
│   │   └── 0
│   └── 1
│       └── 0
├── 3
│   ├── 2
│   │   ├── 1
│   │   │   └── 0
│   │   └── 0
│   ├── 1
│   │   └── 0
│   └── 0
└── 2
    ├── 1
    │   └── 0
    └── 0
```

این درختو تو سایت https://www.text-tree-generator.com/ ساختم که خیلی سایت جالبیه


---

**با تشکر**
**پایان**
محمد حسین روحانی
