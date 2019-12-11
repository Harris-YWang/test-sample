# HackerRank Interview Preparation Kit

----

## Warm-up Challenges

1. [Sock Merchant](https://www.hackerrank.com/challenges/sock-merchant/problem?h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=warmup](https://www.hackerrank.com/challenges/sock-merchant/problem?h_l=interview&playlist_slugs[]=interview-preparation-kit&playlist_slugs[]=warmup)) 袜子商人

   **Input：**

   The first line contains an integer **_n_**, the number of socks represented in **_ar_**.
   The second line contains **_n_** space-separated integers describing the colors **_ar[i]_** of the socks in the pile.

   **Output：**

   Return the total number of *matching pairs* of socks that John can sell.

   ```javascript
   function sockMerchant(n, ar) {
       let tmpArr = [];
       let counter = 0;
       /** Array.prototype.map()和Array.prototype.forEach() 的区别
       	forEach()会改变原始的数组的值，而map()会返回一个全新的数组，原本的数组不受到影响
       	* forEach适合于你并不打算改变数据的时候，而只是想用数据做一些事情 – 比如存入数据库或则打印出来。
       	* map()适用于你要改变数据值的时候。不仅仅在于它更快，而且返回一个新的数组。这样的优点在于你可以使用复合(composition)(map(), filter(), reduce()等组合使用)来玩出更多的花样。
       */
       
       ar.map(value => {
           // 用来判断一个数组是否包含一个指定的值，返回boolean值
           if (tmpArr.includes(value)) {
               // 用来返回数组中第一次出现某个指定的元素位置，从0开始，未找到为-1
               let index = tmpArr.indexOf(value); 
               if (index > -1) {
                   // 在index位置向数组中删除1个item，然后返回被删除的item。
                   tmpArr.splice(index, 1);
               }
               counter++;
           } else {
               // 向数组的末尾添加一个或多个元素，并返回新的长度
               tmpArr.push(value);
           }
       })
       
       return counter;
   }
   ````

2. [Counting Valleys](https://www.hackerrank.com/challenges/counting-valleys/problem?h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=warmup) 数山谷个数

   **Input：**

   The first line contains an integer **_n_**, the number of steps in Gary's hike.

   The second line contains a single string **_s_**, of **_n_** characters that describe his path.

   **Output：**

   Print a single integer that denotes the number of valleys Gary walked through during his hike.
   
   ```javascript
   function countingValleys(n, s) {
          let currentValley = 0;
          let count = 0;
          for (let i = 0; i < n; i++) {
              if (s[i] === 'U') {
                  currentValley++;
              }
              if (s[i] === 'D') {
                  currentValley--;
              }
              if (currentValley == 0 && s[i] === 'U') {
                  count++;
              }
          }
      
          return count;
   }
   ```
   
3. [Jumping on the Clouds](https://www.hackerrank.com/challenges/jumping-on-the-clouds/problem?h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=warmup](https://www.hackerrank.com/challenges/jumping-on-the-clouds/problem?h_l=interview&playlist_slugs[]=interview-preparation-kit&playlist_slugs[]=warmup)) 云上跳跃

   **Input：**

   The first line contains an integer **_n_**, the total number of clouds.

   The second line contains **_n_** space-separated binary integers describing clouds **_c[i]_** where **_0 <= i <= n_**.

   **Output：**

   Print the minimum number of jumps needed to win the game.
   
   ```javascript
   function jumpingOnClouds(c) {
       let jump = 0;
       for (let i = 0; i < c.length;){
           if (c[i + 2] === 0) {
               jump++;
               i += 2;
           } else if (c[i + 1] === 0) {
               jump++;
               i += 1;
           } else {
               i++;
           }
       }
   
       return jump;
   }
   ```

4. [Repeated String](https://www.hackerrank.com/challenges/repeated-string/problem?h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=warmup) 重复的字符串

   **Input：**

   The first line contains a single string, **_s_**.

   The second line contains  an integer **_n_**.

   **Output：**

   Print a single integer denoting the number of letter a's in the first **_n_** letters of the infinite string created by repeating **_s_** infinitely many times.
   
   ```javascript
   function repeatedString(s, n) {
       // 用a来字符串分割成字符串数组，得到字符串中a的个数
       // "aba".split('a') => ["", "b", ""]
       // "aaa".split('a') => ["", "", "", ""]
       // "abab".split('a') => ["", "b", "b"]
       let initialCount = s.split('a').length - 1; 
       /** Math.floor(), Math.ceil(), Math.round()的区别
       	去尾法，进一法，四舍五入法
       */
       let cocent = Math.floor(n / s.length);
       let total = cocent * initialCount;
       let remainder = n % s.length;
       // 提取字符串中从0（包含）到remainder（不包含）的部分
       // "aba".slice(0,0) => ""
       let remaindLetter = s.slice(0, remainder);
       total += remaindLetter.split('a').length - 1;
       return total;
   }
   ```

## Arrays

1. [Arrays: Left Rotation](https://www.hackerrank.com/challenges/ctci-array-left-rotation/problem?h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=arrays](https://www.hackerrank.com/challenges/ctci-array-left-rotation/problem?h_l=interview&playlist_slugs[]=interview-preparation-kit&playlist_slugs[]=arrays)) 数组：左旋
   **Input：**
   
   The first line contains two space-separated integers **_n_** and **_d_**, the size of **_a_** and the number of left rotations you must perform.
    The second line contains **_n_** space-separated integers **_a[i]_**.
   
   **Output：**
   
   Print a single line of **_n_** space-separated integers denoting the final state of the array after performing **_d_** left rotations.

   ```javascript
    function rotLeft(a, d) {
      // 先减后变
      while (d > 0) {
          a.push(a.shift());
          d--;
   };
      return a;
    }
   ```
   
2. [New Year Chaos](https://www.hackerrank.com/challenges/new-year-chaos/problem?h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=arrays](https://www.hackerrank.com/challenges/new-year-chaos/problem?h_l=interview&playlist_slugs[]=interview-preparation-kit&playlist_slugs[]=arrays)) 新年混乱队列
   **Input：**

   The first line contains an integer **_t_**, the number of test cases.

   Each of the next **_t_** pairs of lines are as follows:
   \- The first line contains an integer **_t_**, the number of people in the queue
   \- The second line has **_n_** space-separated integers describing the final state of the queue.

    **_q_**: an array of integers

   **Output：**

   Print an integer denoting the minimum number of bribes needed to get the queue into its final state. Print `Too chaotic` if the state is invalid, i.e. it requires a person to have bribed more than **_2_** people.

   ```javascript
   function minimumBribes(q) {
     let counter = 0;
     let currentPosition = q.length - 1;
     let log = '';
     let bribes;
     // 从后往前计算
     while (currentPosition >= 0) {
       const current = q[currentPosition];
       const orderPosition = currentPosition + 1;
       bribes = current - orderPosition;
       if (bribes >= 3) {
         console.log("Too chaotic")
         return;
       }
       const briberPosition = current - 2;
   
       for (let comparePosition = Math.max(0, briberPosition); comparePosition < currentPosition; comparePosition++) {
         const compare = q[comparePosition]; 
         if (compare > current) {
           counter++;
         }
       }
       currentPosition--;
     }
   
     console.log(counter);
   }
   ```

3. [2D Array - DS](https://www.hackerrank.com/challenges/2d-array/problem?h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=arrays) 2维数组 - 沙漏
   **Input：**

   Each of the **_6_** lines of inputs **_arr[i]_** contains **_6_** space-separated integers **_arr[i] [j]_**.

   **Output：**

   Print the largest (maximum) hourglass sum found in **_arr_**.

   An hourglass in **_A_** to be a subset of values with indices falling in this pattern in **_arr_**'s graphical representation:
   
   a	b	c
   
    	d
   
   e	f	g
   
   ```javascript
   function hourglassSum(arr) {
       let resultArray = [];
       
       for (let currentX = 0; currentX < arr[0].length - 2;) {
           for (let currentY = 0; currentY < arr[0].length -2;) {
               getSum(arr, resultArray, currentX, currentY);
               currentY++;        
           }
           currentX++;
       }
       return Math.max(...resultArray);
   }
   
   
   function getSum(arr, resultArray, currentX, currentY) {
       let shortArray = [];
       for (let i = 0; i < 3; i++) {
           if (i === 1) {
               shortArray[i] = Number(arr[currentY + i][currentX + 1]);
           } else {
               shortArray[i] = arr[currentY + i].slice(currentX, currentX + 3).reduce((acc, val) => acc + Number(val), 0);            
           }
       }
   
       resultArray.push(shortArray.reduce((acc, val) => acc + val, 0))
   }
   ```

4. [Minimum Swaps 2](https://www.hackerrank.com/challenges/minimum-swaps-2/problem?h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=arrays&h_r=next-challenge&h_v=zen) 最小二元交换
   **Input：**

   The first line contains an integer, **_n_**, the size of **_arr_**.
The second line contains **_n_** space-separated integers **_arr[i]_**.
   
   **Output：**
   
   Return the minimum number of swaps to sort the given array.
   
   ```javascript
function minimumSwaps(arr) {
       let obj = {},
           swaps = 0;
       // Copy the array into an object so we don't have to run indexOf a million times
       for(let i = 0; i < arr.length; i++) {
           // The key will be the number and the value will be its position
           obj[arr[i]] = i;
       }
       for(let i = 0; i < arr.length; i++) {
           // Expected number at this spot
           let expectedNumber = i + 1,
               // What it actually is
               actualNumber = arr[i];
           if (actualNumber !== expectedNumber) {
               // Find actual location of the expected number
               let whereToMove = obj[expectedNumber];
               // Update current spot to the expected number
               arr[i] = expectedNumber;
               // Update location of expectedNumber in the object
               obj[expectedNumber] = i;
               // Move actualNumber to where expectedNumber was
               arr[whereToMove] = actualNumber;
               // Update location of actualNumber in the object
               obj[actualNumber] = whereToMove;
               // Increment swaps
               swaps++;
           }
       }
       return swaps;
   }
   ```

5. [Array Manipulation](https://www.hackerrank.com/challenges/crush/problem?h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=arrays) 数组操作
   **Input：**

   The first line contains two space-separated integers **_n_** and **_m_**, the size of the array and the number of operations.
Each of the next lines contains three space-separated integers **_a_**, **_b_** and **_k_**, the left index, right index and summand.
   
   **Output：**
   
   Return the integer maximum value in the finished array.
   
   ```javascript
function arrayManipulation(n, queries) {
   
       let diffs = [];
   
           queries.forEach((value, index) => {
   
                   const range_start = value[0];
                   const range_end = value[1];
                   const addend = value[2];
   
                   if (!diffs[range_start]) {
                           diffs[range_start] = addend;
                   } else {
                           diffs[range_start] += addend; 
                   }
   
                   if (!diffs[range_end + 1]) {
                           diffs[range_end + 1] = 0 - addend;
                   } else {
                           diffs[range_end + 1] -= addend;
                   }
           });
   
           return diffs.reduce((acc, cur) => {
                   return {
                           running_total: acc.running_total + cur,
                           max: Math.max(acc.max, acc.running_total + cur)
                   };
           }, {running_total: 0, max: 0}).max;
   }
   ```
   
## Dictionaries and Hashmaps

1. [Two String](https://www.hackerrank.com/challenges/two-strings/problem?h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=dictionaries-hashmaps) 寻找相同子字符串

   **Input：**

   The first line contains a single integer **_p_**, the number of test cases.
   The following **_p_** pairs of lines are as follows:
   
   * The first line contains string **_s1_**.
   * The second line contains string **_s2_**.
   
   **Output：**
For each pair of strings, return YES or NO.
   
   ```javascript
   function twoStrings(s1, s2) {
   	/**
    	let a = new Set(s1);
   	let b = new Set(s2);
   	
   	for (const letter of b) {
   		if (a.has(letter)) {
   			return "YES";
   		}
   	}
       
   	return "NO";
   */
   	for (let letter of s1) {
   		if (s2.includes(letter)) {
               return 'YES'
           }
       }
   	return 'NO'
   }
   ```
   ```javascript
   function twoStrings(s1, s2) {
   	var map = {};
    	for (let i of s1) {
   		map[i] = 1;
    	}
    	for (let i of s2) {
   		if (map[i])
            return "YES";
    	}
    	return "NO";
   }
   ```

2. [Sherlock and Anagrams](https://www.hackerrank.com/challenges/sherlock-and-anagrams/problem?h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=dictionaries-hashmaps&h_r=next-challenge&h_v=zen) 易位构词游戏

   **Input：**

   The first line contains an integer **_q_**, the number of queries.
   Each of the next **_q_** lines contains a string  to analyze.
   
   **Output：**
   For each query, return the number of unordered anagrammatic pairs.
   
   ```javascript
function sherlockAndAnagrams(s) {
       let anagramCount = 0;
       let currentStringLength = 1;
       let refStrings = [];

       while (currentStringLength < s.length) {
           for (let i = 0; i < s.length - (currentStringLength - 1); i++) {
               let subString = s.slice(i, (i + currentStringLength));
               let preparedSubString = subString.split('').sort().join('');
               refStrings.push(preparedSubString);
           }
           console.log(refStrings);

           while (refStrings.length > 1) {
               let stringToMatch = refStrings.shift();
               refStrings.forEach(element => {
                   if (element === stringToMatch) {
                       anagramCount += 1;
                   }
               });
           }

           refStrings = [];
           currentStringLength++;
       }
       return anagramCount;
}
   ```

3. [Count Triplets](https://www.hackerrank.com/challenges/count-triplets-1/problem?h_l=interview&h_r=next-challenge&h_v=zen&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=dictionaries-hashmaps&h_r=next-challenge&h_v=zen) 易位构词游戏

   **Input：**
   The first line contains two space-separated integers **_n_** and **_r_**, the size of **_arr_** and the common ratio.
   The next line contains **_n_** space-separated integers **_arr[i]_**.
   
   **Output：**
   Return the count of triplets that form a geometric progression.
   
   ```javascript
function countTriplets(arr, r) {
       let len = arr.length //1,1,3,9
       let count = 0
       var m2 = new Map()
    var m3 = new Map()
       arr.forEach((ele) => {
           if (m3.get(ele))
               count = count + m3.get(ele)
   
           if (m2.get(ele))
               m3.set(ele * r, m3.get(ele * r) ? m3.get(ele * r) + m2.get(ele) : m2.get(ele))
   
        m2.set(ele * r, m2.get(ele * r) ? m2.get(ele * r) + 1 : 1)
       })
       return count
   }
   ```
4. [Frequency Queries](https://www.hackerrank.com/challenges/frequency-queries/problem?h_l=interview&h_r=next-challenge&h_r=next-challenge&h_v=zen&h_v=zen&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=dictionaries-hashmaps&h_r=next-challenge&h_v=zen) 频率查询

   **Input：**
   The first line contains of an integer **_q_**, the number of queries.
   Each of the next **_q_** lines contains two integers denoting the 2-d array **_queries_**.
   
   **Output：**
   Return an integer array consisting of all the outputs of queries of type **_3_**.
   
   ```javascript
    function freqQuery(queries) {
   	const result = [];
   	const hash = {};
   	const freq = [];

   	for (let i = 0; i < queries.length; i += 1) {
       	const [action, value] = queries[i];
       	const initValue = hash[value] || 0;

        	if (action === 1) {
           	hash[value] = initValue + 1;
         	freq[initValue] = (freq[initValue] || 0) - 1;
            	freq[initValue + 1] = (freq[initValue + 1] || 0) + 1;
        	}
   
     	if (action === 2 && initValue > 0) {
            	hash[value] = initValue - 1;
            	freq[initValue - 1] += 1;
         	freq[initValue] -= 1;
        	}
   
        	if (action === 3) result.push(freq[value] > 0 ? 1 : 0);
	}
   
   	return result;
};
   ```
5. [Hash Tables: Ransom Note](https://www.hackerrank.com/challenges/ctci-ransom-note/problem?h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=dictionaries-hashmaps) 哈希表：赎金记录

   **Input：**
   The first line contains two space-separated integers, **_m_** and **_n_**, the numbers of words in the **_magazine_** and the **_note_**.
   The second line contains **_m_** space-separated strings, each **_magazine[i]_**.
   The third line contains **_n_** space-separated strings, each **_note[i]_**.
   
   **Output：**
   Print Yes if he can use the magazine to create an untraceable replica of his ransom note. Otherwise, print No.
   
   ```javascript
    function checkMagazine(magazine, note) {
    	let magWordCount = {}
    	magazine.forEach(word => magWordCount[word] = ~~magWordCount[word] + 1)
    	for (let word of note) {
        	if (~~magWordCount[word] <= 0) return console.log('No')
        	magWordCount[word] = ~~magWordCount[word] - 1
    	}
       
    	return console.log('Yes')
    }
   ```
   
## Sorting
1. [Sorting: Bubble Sort](https://www.hackerrank.com/challenges/ctci-bubble-sort/problem?h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=sorting) 排序：冒泡排序

   **Input：**
   The first line contains an integer, **_n_**, the size of the array **_a_**.
   The second line contains **_n_** space-separated integers **_a[i]_**.
   
   **Output：**
   You must print the following three lines of output:
   * Array is sorted in numSwaps swaps., where **_numSwaps_**  is the number of swaps that took place.
   * First Element: firstElement, where **_firstElement_**  is the first element in the sorted array.
   * Last Element: lastElement, where **_lastElement_**  is the last element in the sorted array.
   
   ```javascript
    function countSwaps(a) {
       let swaps = 0
       for (let i = 0; i < a.length; i++) {
           for (let j = 0; j < a.length - 1; j++) {
               // Swap adjacent elements if they are in decreasing order
               if (a[j] > a[j + 1]) {
                   let temp = a[j];
                   a[j] = a[j + 1];
                   a[j + 1] = temp;
                   swaps++
               }
           }
       }
       console.log(`Array is sorted in ${swaps} swaps.`)
       console.log(`First Element: ${a[0]}`)
       console.log(`Last Element: ${a[a.length - 1]}`)
   }
   ```

2. [Mark and Toys](https://www.hackerrank.com/challenges/mark-and-toys/problem?h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=sorting&h_r=next-challenge&h_v=zen) 采购玩具

   **Input：**
   The first line contains two integers, **_n_** and **_k_**, the number of priced toys and the amount Mark has to spend.
   The next line contains **_n_** space-separated integers **_prices[i]_**.
   
   **Output：**
   An integer that denotes the maximum number of toys Mark can buy for his son.
   
   ```javascript
    function maximumToys(prices, k) {
    	let sum = 0;
    	let sorter = prices.sort((a, b) => a - b);
    	let counter = 0;

    	for (var i = 0; i < sorter.length; i++) {
        	if (sorter[i] < k) {
           	 sum += sorter[i];
            	if (sum <= k) {
               	 counter++;
            	} else {
                	break;
            	}
        	}
    	}
       
    return counter;
   }
   ```

3. [Sorting: Comparator](https://www.hackerrank.com/challenges/ctci-comparator-sorting/problem?h_l=interview&h_r=next-challenge&h_v=zen&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=sorting&h_r=next-challenge&h_v=zen) 排序：比较器

   **Input：**
   The first line contains an integer, **_n_**, the number of players.
   Each of the next **_n_** lines contains a player's respective **_name_** and **_score_**, a string and an integer.
   Sample Input:
   
   ```
   5
   amy 100
   david 100
   heraldo 50
   aakansha 75
   aleksa 150
   ```
   **Output：**
   Sort the Player array, and print each sorted element.
Sample Output:
   
   ```
	aleksa 150
	amy 100
	david 100
	aakansha 75
   	heraldo 50
   ```
4. [Fraudulent Activity Notifications](https://www.hackerrank.com/challenges/fraudulent-activity-notifications/problem?h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=sorting) 欺诈性活动提醒

   **Input：**
   The first lined contains two space-separated integers **_n_** and **_d_**, the number of days of transaction data, and the number of trailing days' data used to calculate median spending.
   The second line contains **_n_** space-separated non-negative integers where each integer **_i_** denotesi **_expenditure[i]_**.

   **Output：**
   Print an integer denoting the total number of times the client receives a notification over a period of **_n_** days.

   ```javascript
   function activityNotifications(expenditure, d) {
   
       // Number of notifications
       let n = 0
   
       // Set midpoints for median calculation
       let [i1, i2] = [Math.floor((d - 1) / 2), Math.ceil((d - 1) / 2)]
       let m1, m2, m
   
       // Initialize count sorted subarray
       let cs = new Array(201).fill(0)
       for (let i = d - 1; i >= 0; i--) cs[expenditure[i]]++
   
       // Iterate through expenditures
       for (let i = d, l = expenditure.length; i < l; i++) {
   
           // Find median
           for (let j = 0, k = 0; k <= i1; k += cs[j], j++) m1 = j
           for (let j = 0, k = 0; k <= i2; k += cs[j], j++) m2 = j
           let m = (m1 + m2) / 2
   
           // Check if notification is given
           if (expenditure[i] >= m * 2) n++
   
           // Replace subarray elements
           cs[expenditure[i - d]]--
           cs[expenditure[i]]++
       }
   
       return n
   }
   
   ```

5. [Merge Sort: Counting Inversions](https://www.hackerrank.com/challenges/ctci-merge-sort/problem?h_l=interview&playlist_slugs[]=interview-preparation-kit&playlist_slugs[]=sorting&h_r=next-challenge&h_v=zen) 合并排序：计算倒置

   **Input：**
   The first line contains an integer, , the number of datasets.
   Each of the next  pairs of lines is as follows:
   * The first line contains an integer, **_n_**, the number of elements in **_arr_**.
   * The second line contains **_n_** space-separated integers, **_arr[i]_**.

   **Output：**
   For each of the **_d_** datasets, return the number of inversions that must be swapped to sort the dataset.

   ```javascript
    function countInversions(arr) {
    let inversions = 0;
   
    const mergeSort = function(arr) {
        if (arr.length === 1) {
            return arr;
        }
        const mid = Math.floor(arr.length / 2);
        const left = arr.slice(0, mid);
        const right = arr.slice(mid);
   
        return merge(mergeSort(left), mergeSort(right));
    };
   
    const merge = function(left, right) {
        let result = [];
        let iLeft = 0;
        let iRight = 0;
   
        while (iLeft < left.length && iRight < right.length) {
            if (left[iLeft] > right[iRight]) {
                result.push(right[iRight]);
                iRight++;
                inversions += left.length - iLeft;
            }
            else {
                result.push(left[iLeft]);
                iLeft++;
            }
        }
   
        return result.concat(left.slice(iLeft)).concat(right.slice(iRight));
    };
   
    let result = mergeSort(arr);
    return inversions;
   }
   ```

## String Manipulation
1. [Strings: Making Anagrams](https://www.hackerrank.com/challenges/ctci-making-anagrams/problem?h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=strings) 字谜

   **Input：**
   The first line contains a single string, **_a_**.
   The second line contains a single string, **_b_**.
   
   **Output：**
   Print a single integer denoting the number of characters you must delete to make the two strings anagrams of each other.
   
   ```javascript
    function makeAnagram(a, b) {
    let stringA = new Map()
    let stringB = new Map()
    let count = 0;

    //calculate occurances for each letter in A and B
    for (let i = 0; i < a.length; i++) {
        let char = a[i]
        if (stringA.has(char)) {
            let val = stringA.get(char)
            stringA.set(char, val + 1)
        }
        else stringA.set(char, 1)
    }
    for (let i = 0; i < b.length; i++) {
        let char = b[i]
        if (stringB.has(char)) {
            let val = stringB.get(char)
            stringB.set(char, val + 1)
        }
        else stringB.set(char, 1)
    }

    //Find how much items to remove from A to get it the same as B
    stringA.forEach((value, key) => {
        if (!(stringB.has(key))) {
            //Remove all occurances of this letter since its never in B
            count = count + stringA.get(key)
        }
        else {
            //Get how many times this char occurs in B
            let bOccr = stringB.get(key)
            //Need to remove the difference between what A has and B has
            let diff = value - bOccr
            if (diff > 0) {
                count = count + diff
            }
        }
    })

    //Find how much items to remove from B to get it the same as A
    stringB.forEach((value, key) => {
        if (!(stringA.has(key))) {
            //Remove all occurances of this letter since its never in A
            count = count + stringB.get(key)
        }
        else {
            //Get how many times this char occurs in A
            let aOccr = stringA.get(key)
            //Need to remove the difference between what A has and B has
            let diff = value - aOccr
            if (diff > 0) {
                count = count + diff
            }
        }
    })
    return count
}
   ```
   
2. [Alternating Characters](https://www.hackerrank.com/challenges/alternating-characters/problem?h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=strings&h_r=next-challenge&h_v=zen) 交替字符

   **Input：**
   The first line contains an integer **_q_**, the number of queries.
   The next **_q_** lines each contain a string **_s_**.
   
   **Output：**
   For each query, print the minimum number of deletions required on a new line.
   
   ```javascript
    function alternatingCharacters(s) {
    let deletions = 0;
   
    for (let i = 0; i < s.length; i++) {
        if (s[i] === s[i + 1]) deletions++;
    }
   
    return deletions;
    }
   ```
   
3. [Sherlock and the Valid String](https://www.hackerrank.com/challenges/sherlock-and-valid-string/problem?h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=strings&h_r=next-challenge&h_v=zen&h_r=next-challenge&h_v=zen) 有效字符串
   
   **Input：**
   A single string **_s_**.
   
   **Output：**
   Print YES if string **_s_** is valid, otherwise, print NO.
   
   ```javascript
   function isValid(s) {
    const uni = [... new Set(s.split(''))], rep = []
    uni.forEach(l => {
        let n = s.split('').filter(m => m == l)
        rep.push(n.length)
    })
    let filRep = [... new Set(rep)]

    if (filRep.length > 2) return 'NO'
    let sum = rep.reduce((a, c) => c += a)

    if (Math.floor(sum / rep.length) == (sum / rep.length)) return 'YES'

    let filRepArr = []
    filRep.forEach(n => {
        filRepArr.push(rep.filter(m => m === n).length)
    })

    if (filRepArr.some(l => l == 1) && Math.abs(filRep[1] - filRep[0]) == 1) {
        return "YES"
    }
    return 'NO'
   }
   ```

4. [Special String Again](https://www.hackerrank.com/challenges/special-palindrome-again/problem?h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=strings&h_r=next-challenge&h_v=zen&h_r=next-challenge&h_v=zen&h_r=next-challenge&h_v=zen) 特殊字符串
   
   **Input：**
   The first line contains an integer, **_n_**, the length of **_s_**.
   The second line contains the string **_s_**.
   
   **Output：**
   Print a single line containing the count of total special substrings.
   
   ```javascript
   function substrCount(n, s) {
    let count = n;
    for (let i = 0; i < s.length; i++) {
        let nextIndex = i;
        while (s[i] === s[nextIndex + 1]) nextIndex++;

        if (i !== nextIndex) {
            const length = nextIndex - i;
            count = count + (length * (length + 1)) / 2;
            i = nextIndex;
        } else {
            let step = 1;
            while (s[i + step] === s[i - step] && s[i + step] === s[i + 1]) {
                step++;
                count++;
            }
        }
    }
    return count;
   }
   ```
   
5. [Common Child](https://www.hackerrank.com/challenges/common-child/problem?h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=strings&h_r=next-challenge&h_v=zen&h_r=next-challenge&h_v=zen&h_r=next-challenge&h_v=zen&h_r=next-challenge&h_v=zen) 普通子字符串
   
   **Input：**
   There is one line with two space-separated strings, **_s1_** and **_s2_**.
   
   **Output：**
   Print the length of the longest string **_s_**, such that **_s_** is a child of both **_s1_** and **_s2_**.
   
   ```javascript
   function commonChild(s1, s2) {
    let row = new Array(s1.length + 1).fill(0);

    for (let i = 1; i <= s2.length; i++) {
        for (let j = 1, previousElement = 0; j <= s1.length; j++) {
            let temp = row[j];
            if (s2[i - 1] == s1[j - 1])
                row[j] = previousElement + 1;
            else
                row[j] = Math.max(row[j], row[j - 1])
            previousElement = temp;
        }
    }

    return row.pop();
}
   ```

## Greedy Algorithms

1. [Minimum Absolute Difference in an Array](https://www.hackerrank.com/challenges/minimum-absolute-difference-in-an-array/problem?h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=greedy-algorithms) 数组中的最小绝对值

   **Input：**
   The first line contains a single integer **_n_**, the size of **_arr_**.
   The second line contains **_n_** space-separated integers **_arr[i]_**.

   **Output：**
   Print the minimum absolute difference between any two elements in the array.

   ```javascript
    function minimumAbsoluteDifference(arr) {
    let min = Number.MAX_VALUE;
    arr.sort()
    console.log(arr)
    for (let i = 0; i < arr.length; i++) {
        let num = Math.abs(arr[i] - arr[i + 1])
        if (min > num) {
            min = num
        }
    }
    return min
}
   ```

2. [Luck Balance](https://www.hackerrank.com/challenges/luck-balance/problem?h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=greedy-algorithms&h_r=next-challenge&h_v=zen) 人品守恒

   **Input：**
   The first line contains two space-separated integers **_n_** and **_k_**, the number of preliminary contests and the maximum number of important contests Lena can lose.
   Each of the next **_n_** lines contains two space-separated integers,  **_L[i]_** and **_T[i]_**, the contest's luck balance and its importance rating.

   **Output：**
   Print a single integer denoting the maximum amount of luck Lena can have after all the contests.

   ```javascript
    function luckBalance(k, contests) {
    let important = contests.filter(ar => ar[1] === 1).length;
    let sumAll = contests.reduce((a, b) => a + b[0], 0);
    let sorted = contests.sort((a, b) => a[0] - b[0])
    let win = important - k >= 0 ? important - k : 0
    let min = 0
    for (let i = 0; i < sorted.length; i++) {
        if (win === 0) break;
        if (sorted[i][1] === 0) continue;
        min += sorted[i][0];
        win--
    }
    return sumAll - (2 * min);
}
   ```
   
3. [Greedy Florist](https://www.hackerrank.com/challenges/luck-balance/problem?h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=greedy-algorithms&h_r=next-challenge&h_v=zen) 贪婪的花店

   **Input：**
   The first line contains two space-separated integers **_n_** and **_k_**, the number of flowers and the number of friends.
   The second line contains **_n_** space-separated positive integers **_c[i]_**, the original price of each flower.

   **Output：**
   Print the minimum cost to buy all **_n_** flowers.

   ```javascript
function getMinimumCost(k, c) {

    const arr = c.slice().sort((a, b) => b - a), n = c.length;
    let i = 0, p = 0, sum = 0;
    while (i < n) {
        sum += (p + 1) * arr[i];
        i += 1;
        if (i % k === 0) {
            p += 1;
        }
    }
    return sum;
}
   ```
   
4. [Max Min](https://www.hackerrank.com/challenges/angry-children/problem?h_l=interview&h_r=next-challenge&h_r=next-challenge&h_v=zen&h_v=zen&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=greedy-algorithms&h_r=next-challenge&h_v=zen) 最大值/最小值

   **Input：**
   The first line contains an integer **_n_**, the number of elements in array **_arr_**.
   The second line contains an integer **_k_**.
   Each of the next  lines contains an integer **_arr[i]_** where **_0 <= i < n_**.

   **Output：**
   An integer that denotes the minimum possible value of unfairness.

   ```javascript
function maxMin(k, arr) {
    arr.sort((a, b) => a - b);
    let min = Number.MAX_SAFE_INTEGER;
    for (let i = 0; k - 1 + i < arr.length; i++) {
        min = Math.min(min, arr[k - 1 + i] - arr[0 + i])
    }
    return min
   }
   ```

5. [Reverse Shuffle Merge](https://www.hackerrank.com/challenges/reverse-shuffle-merge/problem?h_l=interview&h_r=next-challenge&h_r=next-challenge&h_v=zen&h_v=zen&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=greedy-algorithms&h_r=next-challenge&h_v=zen&h_r=next-challenge&h_v=zen) 反向随机合并

   **Input：**
   A single line containing the string **_s_**.

   **Output：**
   Find and return the string which is the lexicographically smallest valid **_A_**.

   ```javascript
function reverseShuffleMerge(s) {
    let map = {};
    s = s.split('').reverse('').join('')
    for (let item of s.split('')) {
        map[item] = map[item] ? map[item] + 1 : 1;
    }
    let ref = {}
    for (let key in map) {
        ref[key] = map[key] / 2
    }
    let solution = [], i = 0;
    while (solution.length < s.length / 2) {
        let min_char_pos = -1
        //find the smallest 
        //find the smallest 
        //find the smallest 
        while (true) {
            let c = s[i];
            if (ref[c] > 0 && (min_char_pos < 0 || c < s[min_char_pos])) {
                min_char_pos = i;
            }
            map[c] -= 1;
            if (map[c] < ref[c]) {
                break
            }
            i += 1
        }
        //found the one, restore the count of other
        for (let j = min_char_pos + 1; j < i + 1; j++) {
            map[s[j]] += 1
        }
        //find the smallest 
        //find the smallest 
        //find the smallest 
        ref[s[min_char_pos]] -= 1
        solution.push(s[min_char_pos]);
        i = min_char_pos + 1
    }
    return solution.join('');
}
   ```

## Search
1. [Hash Tables: Ice Cream Parlor](https://www.hackerrank.com/challenges/ctci-ice-cream-parlor/problem?h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=search) 哈希表：冰淇淋店

   **Input：**
   The first line contains an integer, **_t_**, the number of trips to the ice cream parlor.
   Each of the next **_t_** sets of **_3_** lines is as follows:
   * The first line contains **_money_**.
   * The second line contains an integer, **_n_**, the size of the array **_cost_**.
   * The third line contains  space-separated integers denoting the **_cost[i]_**.
   
   **Output：**
   Print two space-separated integers denoting the respective indices for the two distinct flavors they choose to purchase in ascending order. Recall that each ice cream flavor has a unique ID number in the inclusive range from **_1_** to **_|cost|_**.
   
   ```javascript
    function whatFlavors(cost, money) {

    const map = new Map();
    for (let i = 0; i < cost.length; i++) {
        var target = money - cost[i];
        if (map.has(target)) {
            console.log(map.get(target), i + 1);
            break;
        }
        map.set(cost[i], i + 1);

    }
    }
   ```
   
2. [Swap Nodes - Algo](https://www.hackerrank.com/challenges/swap-nodes-algo/problem?h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=search&h_r=next-challenge&h_v=zen) 交换节点

   **Input：**
   The first line contains **_n_**, number of nodes in the tree.
   Each of the next **_n_** lines contains two integers, **_a_**, **_b_**, where **_a_** is the index of left child, and **_b_** is the index of right child of ith node.
   
   * -1 is used to represent a null node.
   
   The next line contains an integer, **_t_**, the size of **_queries_**.
   Each of the next t lines contains an integer **_queries[i]_**, each being a value **_k_**.

   **Output：**
   For each **_k_**, perform the swap operation and store the indices of your in-order traversal to your result array. After all swap operations have been performed, return your result array for printing.

   ```javascript
    function swapNodes(indexes, queries) {
    const depthMap = new Map();
    function buildTree(input) {
    // flatten input array
    input = input.reduce((a,b) => a.concat(b), []);
    class Node {
      constructor(key) {
        this.key = key;
      }
      static Create(key) {
        if (key === -1) return null;
        return new Node(key);
      }
    }
    const tree = new Node(1);
    let currentLevel = [tree];
    let depth = 1;
    while (input.length) {
      let nextLevel = [];
      for (const node of currentLevel) {
        depthMap.set(depth, [...depthMap.get(depth) || [], node]);
        node.left = Node.Create(input.shift());
        node.right = Node.Create(input.shift());
        nextLevel.push(node.left, node.right);
      }
      depth++;
      currentLevel = nextLevel.filter(n => n);
    }
    return tree;
    }
        function traverseInOrder(node) {
    if (!node) return;

    traverseInOrder(node.left);
    queryResult.push(node.key);
    traverseInOrder(node.right);
  }

  const results = [];
  let queryResult;
  const root = buildTree(indexes);
  for (const query of queries) {
    [...depthMap.keys()].filter(depth => depth % query === 0).forEach(depth => {
      depthMap.get(depth).forEach(node => {
        [node.left, node.right] = [node.right, node.left];
      })
    });
    queryResult = [];
    traverseInOrder(root);
    results.push(queryResult);
  }
  return results;
}
   ```