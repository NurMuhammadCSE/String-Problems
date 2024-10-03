# 🚀 Nur Muhammad's Coding Journey: Learning C++ Strings Concepts 📚

Welcome to my daily progress updates where I solve string-related problems in C++! Below are the concepts and problems I’ve worked on.

---

## 🔠 Day 1: First Day Learning

### 1. **🔠Convert Character to Lowercase**

This function converts an uppercase character to lowercase.

```cpp
char toLowerCase(char ch) {
    if (ch >= 'a' && ch <= 'z')
        return ch;
    else {
        char temp = ch - 'A' + 'a';
        return temp;
    }
}
```

### 2. **📝Check Palindrome**

This function checks if a string is a palindrome, considering both uppercase and lowercase characters.

```cpp
bool checkPalindrome(char a[], int n) {
    int s = 0;
    int e = n - 1;
    while (s <= e) {
        if (toLowerCase(a[s]) != toLowerCase(a[e])) {
            return 0;
        } else {
            s++;
            e--;
        }
    }
    return 1;
}
```

### 3. **🔄Reverse a String**

This function reverses a string using two-pointer technique.

```cpp
void reverse(char name[], int n) {
    int s = 0;
    int e = n - 1;
    while (s < e) {
        swap(name[s++], name[e--]);
    }
}
```

### 4. **📏Get String Length**

This function calculates the length of a string.

```cpp
int getLength(char name[]) {
    int count = 0;
    for (int i = 0; name[i] != '\0'; i++) {
        count++;
    }
    return count;
};
```

🔍 Solved Problems

### 1. **🏆Maximum Occurring Character**

Given a string str of lowercase alphabets, the task is to find the character with the maximum occurrence. If more than one character has the maximum frequency, return the lexicographically smaller one.

Example:
Input: str = testsample
Output: e

```cpp
char getMaxOccCharacter(string s) {
    int arr[26] = {0};

    for (int i = 0; i < s.length(); i++) {
        char ch = s[i];
        int number = ch - 'a';
        arr[number]++;
    }

    int maxi = -1, ans = 0;
    for (int i = 0; i < 26; i++) {
        if (maxi < arr[i]) {
            ans = i;
            maxi = arr[i];
        }
    }

    return 'a' + ans;
}
```

### 2. **🧹Remove All Occurrence of a Substring**

Remove all occurrences of a substring part from string s.

Example 1:
Input: s = "daabcbaabcbc", part = "abc"
Output: "dab"

```cpp
class Solution {
public:
    string removeOccurrences(string s, string part) {
        while(s.length() != 0 && s.find(part) < s.length()) {
            s.erase(s.find(part), part.length());
        }
        return s;
    }
};
```

### 3. **🌐Replace Spaces**

Given a string STR, replace all the spaces between words with @40.

Example:
Input: "Coding Ninjas Is A Coding Platform"
Output: "Coding@40Ninjas@40Is@40A@40Coding@40Platform"

```cpp
string replaceSpaces(string &str) {
    string temp = "";
    for(int i=0; i<str.length(); i++) {
        if(str[i] == ' ') {
            temp.push_back('@');
            temp.push_back('4');
            temp.push_back('0');
        } else {
            temp.push_back(str[i]);
        }
    }
    return temp;
}
```

### 4. **🔀Reverse a String (In-Place)**

Reverse the characters of an input string in place.

Example 1:
Input: s = ["h","e","l","l","o"]
Output: ["o","l","l","e","h"]

```cpp
class Solution {
public:
    void reverseString(vector<char>& s) {
        int st = 0;
        int e = s.size() - 1;
        while(st < e) {
            swap(s[st++], s[e--]);
        }
    }
};
```

### 5. **Valid Palindrome**

A phrase is a palindrome if, after removing all non-alphanumeric characters and converting all letters to lowercase, it reads the same forward and backward.

Example 1:
Input: s = "A man, a plan, a canal: Panama"
Output: true

```cpp
class Solution {
private:
    bool valid(char ch) {
        return isalnum(ch);
    }

    char toLowerCase(char ch) {
        if (ch >= 'A' && ch <= 'Z') {
            return ch - 'A' + 'a';
        }
        return ch;
    }

    bool checkPalindrome(string a) {
        int s = 0, e = a.length() - 1;
        while (s <= e) {
            if (a[s] != a[e]) return false;
            s++;
            e--;
        }
        return true;
    }

public:
    bool isPalindrome(string s) {
        string temp = "";
        for (int j = 0; j < s.length(); j++) {
            if (valid(s[j])) temp.push_back(s[j]);
        }

        for (int j = 0; j < temp.length(); j++) {
            temp[j] = toLowerCase(temp[j]);
        }

        return checkPalindrome(temp);
    }
};
```

### 6. **Reverse Words in a String**

Given an input string s, reverse the order of the words.

Example:
Input: s = "the sky is blue"
Output: "blue is sky the"

```cpp
class Solution {
public:
    string reverseWords(string s) {
        vector<string> words;
        stringstream ss(s);
        string tmp;
        while (ss >> tmp) words.push_back(tmp);

        string ans;
        for (int i = words.size() - 1; i >= 0; --i) {
            if (i != words.size() - 1) ans += " ";
            ans += words[i];
        }
        return ans;
    }
};
```

# 🚀 Nur Muhammad's Coding Journey: Day 2 of Learning C++ Strings Concepts 📚

Welcome back to my daily progress updates! Today, I tackled more exciting string-related problems in C++. Let’s dive into what I learned and solved today! 💡 🎯

---

### 1. **🔄 String to Integer (atoi)**

The myAtoi function converts a string to a 32-bit signed integer, handling leading spaces, optional signs, and invalid characters. Here’s the breakdown:

- Ignore Whitespace: Skip any leading spaces.
- Handle Sign: Check for + or - to determine the number's sign.
- Conversion: Read digits until you hit a non-digit character.
- Clamping: Ensure the number is within the 32-bit integer range [-2³¹, 2³¹ - 1].

### Example 1:

- **Input**: `s = "42"`
- **Output**: `42`

### Example 2:

- **Input**: `s = " -042"`
- **Output**: `-42`

```cpp
class Solution {
public:
    int myAtoi(string s) {
        int i = 0, sign = 1;
        long result = 0;

        // Step 1: Skip leading whitespaces
        while (i < s.length() && s[i] == ' ') i++;

        // Step 2: Determine the sign
        if (i < s.length() && (s[i] == '-' || s[i] == '+')) {
            sign = (s[i] == '-') ? -1 : 1;
            i++;
        }

        // Step 3: Convert the digits
        while (i < s.length() && isdigit(s[i])) {
            result = result * 10 + (s[i] - '0');
            // Handle overflow cases
            if (result * sign > INT_MAX) return INT_MAX;
            if (result * sign < INT_MIN) return INT_MIN;
            i++;
        }

        return result * sign;
    }
};
```

## 2. **🔍 Find the First Occurrence in a String**

Given two strings, haystack and needle, this function returns the index of the first occurrence of needle in haystack, or -1 if it doesn't exist.

💻 Example 1:

Input: haystack = "sadbutsad", needle = "sad"
Output: 0

```cpp
class Solution {
public:
    int strStr(string haystack, string needle) {
        int n = haystack.length();
        int m = needle.length();

        if (m == 0)
            return 0; // যদি needle ফাঁকা হয়, আউটপুট 0 হবে

        // haystack এর মধ্যে needle খুঁজে বের করার জন্য লুপ
        for (int i = 0; i <= n - m; i++) {
            // haystack থেকে needle এর দৈর্ঘ্য অনুযায়ী সাবস্ট্রিং মেলাচ্ছি
            if (haystack.substr(i, m) == needle) {
                return i; // যদি মিলে যায়, সেই ইনডেক্স রিটার্ন করবো
            }
        }

        return -1; // যদি না মেলে, -1 রিটার্ন করবো
    }
};
```

## 3. **🔁 Repeated Substring Pattern**

The task is to check if a string s can be formed by repeating a substring multiple times.

💻 Example 1:

Input: s = "abab"
Output: true (because "ab" is repeated)

```cpp
class Solution {
public:
    bool repeatedSubstringPattern(string s) {
        // int n = s.length();

        for (int len = 1; len <= n / 2; len++) {
            if (n % len == 0) {
                string substring = s.substr(0, len);
                string repeated = "";
                for (int i = 0; i < n / len; i++) {
                    repeated += substring;
                }

                if (s == repeated) {
                    return true;
                }
            }
        }
        return false;

        string doubled = s + s; // স্ট্রিংকে দ্বিগুণ করা হলো
        string sub = doubled.substr(
            1, doubled.length() -
                   2); // প্রথম এবং শেষ ক্যারেক্টার বাদ দিয়ে সাবস্ট্রিং নিলাম
        // যদি মূল স্ট্রিংটি নতুন সাবস্ট্রিংয়ে পাওয়া যায়, তাহলে রিপিটেড প্যাটার্ন আছে
        return sub.find(s) != string::npos;
    }
};
```

## **4. Remove Element**

4. Remove Element
   Given an array nums and an integer val, remove all occurrences of val in-place and return the new length of the array.

Example 1:
Input: nums = [3,2,2,3], val = 3
Output: 2, nums = [2,2,_,_]
Example 2:
Input: nums = [0,1,2,2,3,0,4,2], val = 2
Output: 5, nums = [0,1,4,0,3,_,_,_]

```cpp
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int k = 0;
        for(int i=0; i<nums.size(); i++){
            if(nums[i] != val){
                nums[k] = nums[i];
                k++;
            }
        }
        return k;
    }
};
```

## **5. Remove Outermost Parenthesis**

Given a valid parentheses string, return the string after removing the outermost parentheses of every primitive string.

Example 1:
Input: s = "(()())(())"
Output: "()()()"

```cpp
class Solution {
public:
        string removeOuterParentheses(string S) {
        string res;
        int opened = 0;
        for (char c : S) {
            if (c == '(' && opened++ > 0) res += c;
            if (c == ')' && opened-- > 1) res += c;
        }
        return res;
    }
};
```

## **6. Rotate String**

Given two strings s and goal, return true if s can become goal after some number of shifts on s.

Example 1:
Input: s = "abcde", goal = "cdeab"
Output: true

```cpp
class Solution {
public:
    bool rotateString(string s, string goal) {
        if (s.length() != goal.length()) {
            return false;
        }

        string double_s = s + s;

        return double_s.find(goal) != string::npos;
    }
};
```

## **7. Isomorphic String**

Given two strings s and t, determine if they are isomorphic. Characters in s can be replaced to get t.

Example 1:
Input: s = "egg", t = "add"
Output: true

```cpp
class Solution {
public:
    bool isIsomorphic(string s, string t) {
        int m1[256] = {0}, m2[256] = {0}, n = s.size();

        for (int i = 0; i < n; i++) {
            if (m1[s[i]] != m2[t[i]])
                return false;
            m1[s[i]] = i + 1;
            m2[t[i]] = i + 1;
        }
        return true;
    }
};
```

## **8. Largest Odd Number in String**

Given a string num, return the largest-valued odd integer that is a non-empty substring of num, or an empty string if no odd number exists.

Example 1:
Input: num = "52"
Output: "5"

```cpp

class Solution {
public:
    string largestOddNumber(string num) {
        // Start checking from the end of the string
        for (int i = num.length() - 1; i >= 0; i--) {
            // Check if the current character is an odd digit
            if ((num[i] - '0') % 2 == 1) {  // Odd digit found
                // Return the substring from the beginning to the current position (inclusive)
                return num.substr(0, i + 1);
            }
        }
        // If no odd digit is found, return an empty string
        return "";
    }
};

```

Thank You for Following My Journey! 🙌
I am solving string-related problems in C++ every day. Stay tuned for more! 😊
