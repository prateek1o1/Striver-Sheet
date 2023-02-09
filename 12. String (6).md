# STRING

Z FUNCTION
https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/

Brute Force 	
```
class Solution {
public:
    int strStr(string haystack, string needle) {

        int n=haystack.length();
        int m=needle.length();

        if(m>n) return -1;

        int l=0;
        int r=m-1;

        for(int i=0;i<n;i++)
        {
            if(haystack[i]==needle[0])
            {
                int k=0;
                while(k!=m)
                {
                    if(haystack[i+k]==needle[k])
                            k++;
                    else
                        break; 
                }
                if(k==m) return i;
            }
        }
        return -1;
    }
};
```
$O(N*M)$

Z Algorithm
```
class Solution {
private:
    vector<int> Z(string &s) {
        vector<int> z(s.size());
        int l = 0, r = 1;
		
   for (int i = 1; i < s.size(); ++i) {
        z[i] = i > r ? 0 : min(r - i, z[i - l]);

  	while (i + z[i] < s.size() && s[z[i]] == s[z[i] + i])
                ++z[i];

            if (z[i] + i > r) {
               l = i;
               r = z[i] + i;
            }
        }
        return z;
    }
	
public:
    int strStr(string haystack, string needle) {
        if ((int) needle.size() == 0) 
            return 0;
        
        int N = int(haystack.size());
        int M = int(needle.size());
        string new_s = needle + "$" + haystack;
        vector<int> z = Z(new_s);

        for (int i = 0; i < N + M + 1; i++) 
            if (z[i] == M) 
                return i - M - 1;

        return -1;
    }
};
```
$O(N+M)$

KMP ALGORITHM/LPS(π) ARRAY
https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/

```
class Solution {
public:
    int strStr(string haystack, string needle) {
        int m = haystack.size(), n = needle.size();
        if (!n) {
            return 0;
        }
        vector<int> lps = kmpProcess(needle);
        for (int i = 0, j = 0; i < m;) {
            if (haystack[i] == needle[j]) { 
                i++, j++;
            }
            if (j == n) {
                return i - j;
            }
            if (i < m && haystack[i] != needle[j]) {
                j ? j = lps[j - 1] : i++;
            }
        }
        return -1;
    }
private:
    vector<int> kmpProcess(string needle) {
        int n = needle.size();
        vector<int> lps(n, 0);
        for (int i = 1, len = 0; i < n;) {
            if (needle[i] == needle[len]) {
                lps[i++] = ++len;
            } else if (len) {
                len = lps[len - 1];
            } else {
                lps[i++] = 0;
            }
        }
        return lps;
    }
};
```
$O(N+M)$


MINIMUM CHARACTERS NEEDED TO BE INSERTED IN THE BEGINNING TO MAKE IT PALINDROMIC
https://www.interviewbit.com/problems/minimum-characters-required-to-make-a-string-palindromic/

```
vector<int> computeLPSArray(string str) {
    int M = str.length();
    vector<int> lps(M);
    int len = 0;
    lps[0] = 0;
    int i = 1;
    while (i < M) {
        if (str[i] == str[len]) {
            len++;
            lps[i] = len;
            i++;
        }
        else {
            if (len != 0) {
                len = lps[len-1];

            }
            else {
                lps[i] = 0;
                i++;
            }
        }
    }
    return lps;
}

int Solution::solve(string str) {
    assert(str.size() >= 1 && str.size() <= 1e6); 
    string revStr = str;
    reverse(revStr.begin(), revStr.end());
    string concat = str + "$" + revStr;
    vector<int> lps = computeLPSArray(concat);
    return (str.length() - lps.back());
}
```

CHECK FOR ANAGRAMS
https://leetcode.com/problems/valid-anagram/

```
class Solution {
public:
    bool isAnagram(string s, string t) {
        int count[26]={0};
        int n=s.size();
        if(s.size()!=t.size()) return false;
        for(int i=0;i<n;i++)
        {
            count[s[i]-'a']++;
            count[t[i]-'a']--;
        }

        for(int i=0;i<26;i++)
        {
            if(count[i]!=0)
                return false;
        }
        return true;
    }
};
```
COUNT AND SAY
https://leetcode.com/problems/count-and-say/

```
class Solution {
public:
    string countAndSay(int n) {

        if(n==1)
            return "1";

        string X=countAndSay(n-1);
        int last=X.length();
        int i=0;
        int count=0;
        string s="";

        while(i<last)
        {
            char ch=X[i];
            int nch=0;

            while(i<last && X[i]==ch)
            {
                nch+=1;
                i++;
            }
            s+=to_string(nch);
            s+=ch;
        }
        return s;
    }   
};
```

COMPARE VERSION NUMERS
https://leetcode.com/problems/compare-version-numbers/

```
class Solution {
public:
    int compareVersion(string version1, string version2) {
        
        int n=version1.length();
        int m=version2.length();
        int i=0,j=0; 

        while(i<n || j<m)
        {
            int A=0;
            int B=0;
            while(i<n && version1[i]!='.')
            {
                A=A*10+(version1[i++]-'0');
            }

            while(j<m && version2[j]!='.')
            {
                B=B*10+(version2[j++]-'0');
            }

            if(A < B) return -1;

            else if(A > B) return 1;
            i++; j++;
        }
        return 0;
    }
};
```