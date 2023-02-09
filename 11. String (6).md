# STRING

REVERSE WORDS IN A STRING
https://leetcode.com/problems/reverse-words-in-a-string/
### Done using stack!
```
class Solution {
public:
    string reverseWords(string s) {
        
    stack<string> store;
    string k;
    for(int i=0;i<s.size();i++)
    {
        if(s[i]==' ') continue;
        while(i<s.size() && s[i]!=' ') k+=s[i++];
        store.push(k);
        k="";
    }
    string answer="";
    while(!store.empty())
    {
        answer+=store.top();
        store.pop();
        if(!store.empty())
            answer+=" ";
    }
    return answer;
    }
};
```
LONGEST PALINDROME IN A STRING
https://leetcode.com/problems/longest-palindromic-substring/
```
class Solution {
public:
    string longestPalindrome(string s) {
        int N=s.size();

        if(N==0) return "";
        bool dp[N][N];
        memset(dp,0,sizeof(dp));

        string answer;
        answer+=s[0];

        for(int i=0;i<N;i++)
            dp[i][i]=true;

        for(int i=N-1;i>=0;i--)
        {
            for(int j=i+1;j<N;j++)
            {
                if(s[i]==s[j])
                {
                    if(j-i==1 || dp[i+1][j-1])
                    {
                    dp[i][j]=true;
                    if(answer.size()<j-i+1)
                        {
                        answer=s.substr(i,j-i+1);
                        }
                    }
                }
            }
        }
        return answer;
    }
};
```
ROMAN NUMBER TO INTEGER AND VICE VERSA
https://leetcode.com/problems/roman-to-integer/
```
class Solution {
public:
    int romanToInt(string s) {
        unordered_map<char,int> Roman=
        { {'I',1},{'V',5},{'X',10},{'L',50},{'C',100},{'D',500},{'M',1000}};
        int N=s.size();
        int answer = Roman[s[N-1]];

        for(int i=s.size()-2;i>=0;i--)
        {
            if(Roman[s[i]] < Roman[s[i+1]])
            {
                answer-=Roman[s[i]];
            }
            else
            {
                answer+=Roman[s[i]];
            }
        }
        return answer;
    }
};
```
IMPLEMENT ATOI/STRSTR
https://leetcode.com/problems/string-to-integer-atoi/
```
class Solution {
public:
    int myAtoi(string s) {
        int sign=1,i=0;
        while(s[i]==' ') i++;
        
        if(s[i]=='-' || s[i]=='+')
        {
            sign=1-2* (s[i++]=='-');
        }
        int base=0;
        while(s[i]>='0' && s[i]<='9')
        {
            int R=s[i++]-'0';
            if( base > INT_MAX/10 || (base == INT_MAX/10 && R>7) )
            {
                if(sign==-1) return INT_MIN;
                else return INT_MAX;
            }
            base=10*base + R;
        }
        return sign*base;
    }
};
```
LONGEST COMMON PREFIX
https://leetcode.com/problems/longest-common-prefix/
```
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        
        if(strs.size()==1) return strs[0];
        string C=strs[0];
        for(int i=1;i<strs.size();i++)
        {
            string A=strs[i];
            string T;
            for(int j=0;j<min(A.size(),C.size());j++)
            {
                if(A[j]==C[j]) T+=A[j];
                else break;
            }
            if(C.size()>=T.size())
            {
                C=T;
            }    
        }
        return C;
    }
};
```
RABIN KARP
https://leetcode.com/problems/repeated-string-match/
```
class Solution {
public:
    int repeatedStringMatch(string a, string b) {

       for(int i=0,j=0;i<a.size();++i) 
       {
           for(j=0;j<b.size() && a[(i+j)%a.size()]==b[j];++j);

           if(j==b.size()) return (i+j-1)/a.size() +1;

       }
       return -1;
    }
};
```
