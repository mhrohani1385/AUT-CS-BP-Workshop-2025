### نوشته شده در نرم افزار obsidian با markdown
---
## سوال اول - دلم تنگ شد

```c
#include <stdio.h>   

// Code by mhr85

int main() {

    int n;
    scanf("%d", &n);

    int arr[n];
	
	// geting input
    for(int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }
    
    for(int i = n - 1; i >= 0; i--){
        printf("%d", arr[i]);
        // inserting space after each one but last one
        if (i != 0) {
            printf(" ");
        }
    }

    printf("\n");

}
```

چاپ را از آخرین اندیس شروع کرده تا اولین اندیس (0) ادامه داده ایم.

## سوال دوم - ولم کن

```c
#include <stdio.h>   
#include <math.h>

// Code by mhr85

int isPrime(int n) {

    // checking 1; 1 is not prime.
    if (n == 1) return 0;

    // checking 2
    if (n != 2 && n % 2 == 0)
    {
        return 0;
    }

    // checking odd numbers only after checking 2
    for(int i = 3; i <= sqrt(n); i += 2) {
        
        if (n % i == 0)
        {
            return 0;
        }
        
    }

    return 1;

}

int main() {

    int i;
    scanf("%d",&i);

    int checked_primes_count = 0;
    int checking_number = 0;

    while (checked_primes_count < i)
    {
        if (isPrime(++checking_number))
        {
            checked_primes_count+=1;
        }
    }

    printf("%d\n", checking_number);

    return 0;

}
```

تابع isPrime فقط بررسی می کند که آیا ورودی اش عددی اول است یا نه. ما در یک حلقه از ۱ شروع کرده و بررسی می کنیم که آیا عدد اول است یا نه؟ سپس اگر اول بود به شمارنده ای که نشان می دهد تا الان چند عدد اول پیدا کردیم checked_primes_count یکی اضافه می کنیم و این کار را ادامه می دهیم تا اعداد اول به تعداد مورد نظر پیدا کرده باشیم.

## سوال سوم - شکلات

```c
#include <stdio.h>   

// Code by mhr85

int main() {

    int n;
    scanf("%d", &n);

    unsigned int arr[n];
    
    unsigned int sum = 0;
    for (unsigned i = 0; i < n; i++)
    {
        scanf("%d", &arr[i]);
        sum += arr[i];
    }
    
    int index;
    int saamaanSum = 0;
    for (index = 0; saamaanSum * 2 < sum; index++)
    {
        saamaanSum += arr[index];
    }
    
    if (saamaanSum * 2 == sum)
    {
        printf("%d %d\n", index, index+1);
    }
    else
    {
        printf("-1\n");
    }
    
}
```

جمع همه را در sum محاسبه می کنیم و سپس دوباره از اول شروع به جمع کردن می کنیم و جمع جدید را در saamaanSum ذخیره می کنیم و این جمع کردن را تا زمانی که دو برابر saamaanSum از sum کمتر است ادامه می دهیم. وقتی که از این شرط عبور کرده و از حلقه خارج شدیم بررسی می کنیم که دو برابر saamaanSum برابر با sum است یا بزرگ تر از آن. اگر برابر باشد یعنی می توانیم شکلات را نصف کنیم.

## سوال چهارم - محاسبه مد

```c
#include <stdio.h>   

// Code by mhr85

int exists(int* arr, unsigned int size, int whatExist) {
    for (unsigned i = 0; i < size; i++)
    {
        if (arr[i] == whatExist)
        {
            return i;
        }
    }
    return -1;
}

int main() {

    int n;
    scanf("%d", &n);

    if (n == 0)
    {
        return 0;
    }
    

    int nums[n]; // at max we have n non repeated numbers.
    int repeats[n];

    int arraySize = 0;

    for (unsigned i = 0; i < n; i++)
    {
        int input;
        scanf("%d", &input);

        int indexInArray = exists(nums, arraySize, input);

        // not exists
        if (indexInArray == -1)
        {
            nums[arraySize] = input;
            repeats[arraySize] = 1;
            arraySize++;
        } else {
            repeats[indexInArray]++;
        }
    }

    int maxIndex = 0, max = repeats[0];
    for (unsigned i = 1; i < arraySize; i++)
    {
        if (repeats[i] > max)
        {
            maxIndex = i;
            max = repeats[i];
        }
    }

    printf("%d\n", nums[maxIndex]);

    return 0;
    
}
```

یک آرایه nums داریم و یک آرایه repeats
قرار است یک شکل مشابه این بسازیم: مثلا به ازای ورودی زیر:

```
7 2 12 1 3 4 2 5 2 4
```

خواهیم داشت:

| nums :: | repeats :: |
| ------- | ---------- |
| 7       | 1          |
| 2       | 3          |
| 12      | 1          |
| 1       | 1          |
| 3       | 1          |
| 4       | 2          |
| 5       | 1          |
برای ساخت این آرایه ها نیاز است به ازای هر عدد ورودی این کار را بکنیم:
چک کنیم ببینیم آیا در nums موجود است یا نه؟ اگه بود که به repeats موجود در لیست یکی اضافه می کنیم. در غیر این صورت عدد را در nums قرار داده و مقدار متناظر آنرا در repeats برابر با یک قرار می دهیم.
اندازه آرایه ها را با n برابر قرار داده ایم چون در بدترین حالت هر عدد یک بار تکرار شده و باید یک خانه در nums به آن اختصاص یابد.

تابع exists چک می کند که آیا مقدار مشخصی در یک آرایه وجود دارد یا نه؟ و اگر وجود نداشته باشد منفی یک بر می گرداند در غیر اینصورت اندیس مربوط به آن مقدار در آرایه را بر می گرداند.

در نهایت بیشترین repeats را پیدا کرده و عدد متناظر با آنرا چاپ می کنیم.
## سوال پنجم - چقدررر عدد

```c
#include <stdio.h>   

// Code by mhr85

unsigned int count2(unsigned a) {
    unsigned int count = 0;
    
    while (a != 0)
    {
        if (a % 10 == 2)
        {
            count++;
        }
        a /= 10;
    }
    
    return count;
}

int main() {

    unsigned int a, b;
    scanf("%u %u", &a, &b);

    unsigned int sum = 0;
    for (unsigned i = a; i <= b; i++)
    {
        sum += count2(i);
    }
    
    printf("%d\n", sum);

}
```

تابع count2 تعداد ارقام 2 موجود در یک عدد را می شمارد. سپس در یک حلقه از عدد اول شروع می کنیم و تا آخرین عدد تعداد دو ها را شمرده و با هم جمع می زنیم.
## سوال ششم - رتبه یه چیز شخصیه

```c
#include <stdio.h>
#include <time.h>

// to check running time and printing the algorithm prograccing notes change it to 1

#define DEBUG 0

// Code by mhr85

void printArray(const int *array, unsigned size)
{
    for (unsigned i = 0; i < size; i++)
    {
        printf("%d ", array[i]);
    }
    printf("\n");
}

void replaceWith(const int *indexes, unsigned indexesCount, int replaceWith, int *array)
{
    for (unsigned i = 0; i < indexesCount; i++)
    {
        array[indexes[i]] = replaceWith;
    }
}

void fillRankArray(const int *sourceArray, int *rankArray, unsigned size)
{

    // copy array
    int array[size];
    for (unsigned i = 0; i < size; i++)
    {
        array[i] = sourceArray[i];
    }

    if (DEBUG)
    {
        printf("fillRankArray For:\n");
        printArray(array, size);
    }

    unsigned short currentRankingLevel = 1;

    _Bool isRankingComplited = 0;

    while (!isRankingComplited)
    {

        int max = -1;
        unsigned currentMaxCount = 0;
        unsigned currentMaxIndexes[size];

        for (unsigned i = 0; i < size; i++)
        {
            int checkingValue = array[i];
            if (checkingValue > max)
            {
                max = checkingValue;
                currentMaxCount = 1;
                currentMaxIndexes[0] = i;
            }
            else if (checkingValue == max && max != -1)
            {
                currentMaxCount += 1;
                currentMaxIndexes[currentMaxCount - 1] = i;
            }

            if (DEBUG)
            {
                printf("in for checking %d, max %d:\n", checkingValue, max);
                printArray(currentMaxIndexes, currentMaxCount);
            }
        }

        if (max == -1)
        {
            isRankingComplited = 1;
        }
        else
        {
            // replace current max in array with -1
            replaceWith(currentMaxIndexes, currentMaxCount, -1, array);
            // replace current max indexes with their rank in rankArray
            replaceWith(currentMaxIndexes, currentMaxCount, currentRankingLevel, rankArray);

            if (DEBUG)
            {
                printf("ARRAY:\n");
                printArray(array, size);

                printf("RANK ARRAY:\n");
                printArray(rankArray, size);
            }

            currentRankingLevel += currentMaxCount;
        }
    }
}

int program()
{

    int n;
    scanf("%d", &n);

    int arr[n];

    for (unsigned i = 0; i < n; i++)
    {
        scanf("%d", &arr[i]);
    }

    int rankArray[n];
    fillRankArray(arr, rankArray, n);

    for (unsigned i = 0; i < n; i++)
    {
        printf("%d", rankArray[i]);
        if (i != n - 1)
        {
            // inserting space after each one but last one
            printf(" ");
        }
    }

    if (n != 0)
    {
        printf("\n");
    }

    return 0;
}

int main()
{

    if (DEBUG)
    {

        clock_t c_start = clock();
        int result = program();
        clock_t c_end = clock();

        float p_time = (c_end - c_start) * 1000 / (float)CLOCKS_PER_SEC;
        printf("\nProgram running time ms : %.3f\n", p_time);

        return result;
    }
    else
    {

        return program();
    }
}
```

یک تابع جدا به اسم fillRankArray ساخته ایم که کار اصلی برنامه را انجام می دهد. بقیه برنامه گرفتن ورودی و دادن آن به تابع و سپس چاپ خروجی تابع است.

توضیحات این تابع:
ابتدا دو آرایه ورودی گرفته ایم که یکی اعداد مورد نظر و دومی آرایه خروجی برای ذخیره مقادیر در آن است (در آن رتبه عدد ها را ذخیره می کنیم).
در مرحله اول آرایه ورودی sourceArray را کپی می کنیم تا تغییر آن منجر به تغییر آرایه ورودی نشود و تابع استقلال ورودی اش را حفظ کند. البته با تعریف پوینت به صورت const int * جلو آنرا گرفتیم ولی لازم است در یک آرایه موقت اعداد را تغییر داده و پس از تعیین هر رتبه مقادیر آنرا با منفی یک جایگذاری کنیم.
سپس یک while به همراه یک فلگ استفاده می کنیم که تا زمانی که همه آرایه با منفی یک برابر نشده و رتبه دهی نشده ادامه پیدا می کند.

سپس درون این while از یک for استفاده می کنیم که در تمام مقادیر آرایه موقتمان پیمایش می کند و بزرگ ترین مقدار و اندیس های تکرار آنرا پیدا می کند. پس از اتمام فور مشخص می شود که چه اندیس هایی باید با منفی یک جایگذاری شوند و رتبه مورد نظر در rankArray به آنها اختصاص پیدا کند. اینکار را با تابع replaceWith انجام می دهیم. مقادیر مورد نظر که در حال رتبه دهی به آنها هستیم را در array با منفی یک جایگذاری کرده و در rankArray هم مقادیر را با رتبه مورد نظر جایگذاری می کنیم. دقت کنید که این تابع مقادیر را در آرایه داده شده replace نمی کند در حقیقت کاری که می کند این است که یک لیست ایندکس می گیرد و تمام آن اندیس ها را در آرایه داده شده را با مقدار داده شده مقدار دهی می کند.
اینکه چه رتبه ای باید اختصاص پیدا کند به وسیله متغیر currentRankingLevel انجام می شود که در عمل می شمرد که در چندیم چرخش while هستیم و تا الان چه رتبه هایی اختصاص پیدا کرده.
بعد از اینکه تمام مقادیر در آرایه موقت منفی یک شدند از وایل خارج شده و تابع که void است بر می گردد. در ادامه ما لیست رتبه ها را متناظر نمره ها داریم. حال کافی است چاپ را انجام دهیم!
## سوال هفتم - این که بین پکینگه

```c
#include <stdio.h>   

// Code by mhr85

int main() {

    unsigned int n, c;
    scanf("%u %u", &n, &c);

    unsigned int temp_sum = 0;
    unsigned int out = 0;

    for (unsigned int i = 0; i < n; i++)
    {
        unsigned int in;
        scanf("%u", &in);
        if (temp_sum + in > c)
        {
            temp_sum = 0;
            out++;
        }
        temp_sum += in;
    }

	// check if is there any one remainded to get picture or not
    if (temp_sum > 0)
    {
        out++;
    }
    

    printf("%u\n", out);

    return 0;

}
```

متغیر temp_sum ظرفیت پر شده از عکس فعلی را مشخص می کند. در `if (temp_sum + in > c)` بررسی می کنیم که اگر مقدار ظرفیت پر شده از عکس از ظرفیت دوربین بیشتر بود یک عکس جدید اضافه کرده و temp_sum را برابر صفر کنیم زیرا داریم یک عکس جدید می گیریم و سپس فرایند اضافه کردن فرد را به عکس ادامه دهیم (`;temp_sum += i`) 

در آخر چک می کنیم که اگه شخصی در عکس اضافه شده باشد (ظرفیت پر شده از عکس فرضی که داریم می گیریم صفر نباشد به این معنی که کسی در عکس موجود باشد) یک عکس به تعداد عکس ها اضافه کنیم.
## سوال هشتم - ضرب ماتریس ها

```c
#include <stdio.h>

// Code by mhr85

int main()
{

    unsigned int a, b, c;
    scanf("%d %d %d", &a, &b, &c);

    // first matris is a x b
    int firstMatris[b][a]; // i, j

    for (unsigned j = 0; j < a; j++)
    {
        for (unsigned i = 0; i < b; i++)
        {
            scanf("%d", &firstMatris[i][j]);
        }
    }

    // second matris is b x c
    int secondMatris[c][b]; // i, j

    for (unsigned j = 0; j < b; j++)
    {
        for (unsigned i = 0; i < c; i++)
        {
            scanf("%d", &secondMatris[i][j]);
        }
    }

    // multiplaction result is a x c
    int result[c][a];

    // loop in first matris rows
    for (unsigned j1 = 0; j1 < a; j1++)
    {

        // loop in second matris columns
        for (unsigned i2 = 0; i2 < c; i2++)
        {

            int sum = 0;
            int i1, j2;
            // multiplaction; adapter is equel to j2 and i1
            for (unsigned adapter = 0; adapter < b; adapter++)
            {
                i1 = j2 = adapter;
                sum += firstMatris[i1][j1] * secondMatris[i2][j2];
            }

            result[i2][j1] = sum;
        }
    }

    // printing result matris
    for (unsigned j = 0; j < a; j++)
    {
        for (unsigned i = 0; i < c; i++)
        {
            printf("%d", result[i][j]);
            if (i != c - 1)
            {
                printf(" ");
            }
        }
        printf("\n");
    }
    
}
```

بیشتر برنامه گرفتن و ذخیره کردن ماتریس ها و چاپ آنهاست. اصل فرایند ضرب کردن ماتریس ها در سه  for تو در تو انجام می شود(در کد کامنت `multiplaction result is a x c` را ببینید)

دقت کنید که ما سطر j ام ماتریس اول را در ستون i ام ماتریس دوم ضرب می کنیم (j1 , i2) 
حال باید بدانید که تعداد اعضای سطر j ام ماتریس اول و ستون i ام ماتریس دوم برابر و برابر با b است. پس باید یک for داشته باشیم که b بار ضرب انجام داده و مجموع این حاصل ضرب ها به ما یک درایه از ماتریس خروجی را می دهد که درایه سطر j و ستون i آن است.
ماتریس ها را طوری ذخیره کردیم که `matris[i][j]` به معنی درایه ستون i ام و سطر j ام است.
هر مقداری که ضرب دو درایه است، باید به اینگونه باشد:
ما درحال ضرب سطر های ماتریس اول در ستون های ماتریس دوم هستیم. در هر مرحله که برای تعیین یک درایه ماتریس خروجی انجام می شود ما درون فور دوم هستیم.

حال ما باید در سطر مورد نظر که در حال ضرب هستیم از اولین آیتم با شماره ستون اول یعنی i اول شروع کنیم.
و برای ستون موردن نظر که در حال ضرب سطر در آن هستیم باید از اولین آیتم با شماره سطر اول یعنی j اول شروع کنیم. 
پس ما یک متغییر آداپتر مشخص می کنیم که شماره ستون در سطر ماتریس اول یعنی i1 و شماره سطر در ستون ماتریس دوم یعنی j2 را مشخص کند که این دو برابر اند.

## سوال نهم - MERGE

```c
#include <stdio.h>

// Code by mhr85

int main()
{

    int aSize, bSize;
    scanf("%d %d", &aSize, &bSize);

    int a[aSize], b[bSize];

    // input a
    for (unsigned i = 0; i < aSize; i++)
    {
        scanf("%d", &a[i]);
    }

    // input b
    for (unsigned i = 0; i < bSize; i++)
    {
        scanf("%d", &b[i]);
    }


    int aI = 0, bI = 0;
    int resultSize = aSize + bSize;

    for (unsigned iR = 0; iR < resultSize; iR++)
    {

        //  b is ended and all b is printed
        //  ^^^^^^^^^^^
        if ((aI != aSize) && (bI == bSize || a[aI] <= b[bI]))
        {
            printf("%d ", a[aI++]);
        } else {
            printf("%d ", b[bI++]);
        }
        
    }

    printf("\n");

}
```

همان فرایند ورودی گرفتن برای همه سوال ها اینجا هم هست.
اصل فرایند در فور آخر انجام میشه. متغیر iR یا اندیس ریزالت فقط برای تعیین تعداد چرخش در فور هست و ازش استفاده دیگه ای نشده.

دو نشانگر aI و bI استفاده شدن که نشون میدن a و b مورد بررسی و مقایسه در حال حاضر کدومان.

توی فور یه ایف نوشتیم که یه سری چیزو چک می کنه.

- اول اینکه آیا aI که نشانگر مربوط به لیست a هست به آخرین آیتم لیست a اشاره می کند یا نه.
	- اگر اشاره نمی کرد بقیه ایف چک می شد و اگر نه می رفتیم به الس و چون ما آخرین a رو چاپ کرده بودیم و اندیس aI از اندیس های قابل قبول زده بیرون یعنی فقط b ها برای چاپ موندن و از لیست b بر می داریم و چاپ می کنیم.
	- ولی اگه اشاره نمی کرد که باید بقیه ایف رو چک می کردیم:
		- حالا اگه آخرین b رو چاپ کرده بودیم
		- یا اینکه a مورد بررسی از b مورد بررسی کوچیکتر بود:
			- یعنی باید a رو چاپ کنیم و نشانگر رو یکی جلو بدیم.
			اگه یکی از دو شرط بالا نقض می شد دوباره می رفتیم تو الس و b مورد بررسی رو چاپ می کردیم


## سوال دهم - در خواب پولدار شو!

```c
#include <stdio.h>

// Code by mhr85

// for solving this sequence, we need to split the inputs into increasing sequences.

int main()
{
    
    unsigned int n;
    scanf("%u", &n);

    unsigned arr[n];

    for (unsigned i = 0; i < n; i++)
    {
        scanf("%u", &arr[i]);
    }

    int maxProfit = 0;
    
    unsigned int bestBuyDay = 1, bestSellDay = 1;

    for (unsigned i = 0; i < n; i++)
    {

        int buyPrice = arr[i];
        int maxProfitForThisBuy = 0;
        unsigned int bestSellingDateForThisBuy = i;

        for (unsigned j = i + 1; j < n; j++)
        {

            // sell price - buy price
            int diff = arr[j] - buyPrice;

            if (diff > maxProfitForThisBuy)
            {
                bestSellingDateForThisBuy = j + 1;
                maxProfitForThisBuy = diff;
            }
            
        }

        if (maxProfitForThisBuy > maxProfit)
        {
            bestBuyDay = i + 1;
            bestSellDay = bestSellingDateForThisBuy;
            maxProfit = maxProfitForThisBuy;
        }

    }
    

    if (maxProfit != 0)
    {
        printf("%d %d\n", bestBuyDay, bestSellDay);
    } else {
        printf("%d\n", -1);
    }

}
```

نیازی به توضیح نیست. طبق هینت سوال برای هر روز خرید بهترین روز فروش رو مشخص می کنیم و در نهایت با بهترین سود روز های خرید دیگه مقایسه می کنیم و از بین روز های خرید بهترین مشخص میشه و متناظر به اون بهترین روز فروش برای اون خرید.

---

**با تشکر**
**پایان**
محمد حسین روحانی
