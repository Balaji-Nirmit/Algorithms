# Algorithms
algorithms

# checking if a character is present in string in java
```java
class Main{
    public static void main(String[] args){
        String str="aeiou";
        int i=0,e=str.length();
        System.out.println(str.indexOf('i')==1);
    }
}
```

# Knuth Moris Pratt Algorithm
## longest prefix suffix

```java
class Main {
    public static void main(String[] args) {
        // Input string
        String str = "abcabdabcabcabd";
        
        // Array to store the prefix function values
        int[] arr = new int[str.length()];
        
        // Initializing the first element
        arr[0] = 0;
        
        int pre = 0, suf = 1; // Variables to track prefix and suffix
        while (suf < str.length()) {
            // If characters at pre and suf positions are equal
            if (str.charAt(pre) == str.charAt(suf)) {
                arr[suf] = pre + 1; // Store the length of the matched prefix
                pre++;               // Move pre forward
                suf++;               // Move suf forward
            } else {
                // If there's no match and pre is at the beginning
                if (pre == 0) {
                    arr[suf] = 0; // No prefix match for this character
                    suf++;        // Move suf forward
                } else {
                    pre = arr[pre - 1]; // Use the previous prefix length to shift pre
                }
            }
        }
        
        // Output the last value in the array (prefix function)
        System.out.println(arr[str.length() - 1]);
    }
}
```

## string matching using KMP

```java
class Main{
    public static void main(String[] args){
        String str="onionionson";
        String st="onion1s";
        // finding the LPS for the st
        int[] arr=new int[st.length()];
        arr[0]=0;
        int pre=0,suf=1;
        while(suf<st.length()){
            if(st.charAt(pre)==st.charAt(pre)){
                arr[suf]=pre+1;
                pre++;
                suf++;
            }
            else{
                if(pre==0){
                    arr[suf]=pre+1;
                    suf++;
                }
                else{
                    pre=arr[pre-1];
                }
            }
        }
        // now matching 
        int first=0,second=0;
        while(second<st.length() && first<str.length()){
            if(st.charAt(second)==str.charAt(first)){
                first++;
                second++;
            }
            else{
                if(second==0){
                    first++;
                }
                else{
                    second=arr[second-1];
                }
            }
        }
        // output index
        if(second==st.length()){
            System.out.println(first-second);
        }
        // here if second == st.length then loop breaks since got the answer;
        // if the loops breaks and second !=st.length which means that loop breaks due to
        // str being traversed completely. which means nothing is found
        else{
            System.out.println(-1);
        }
    }
}
```


# checking if string is rotated or not

say we have a string str1="nirmit"
and str2="rmitni"
and str3="itnirm"
when we rotate str1 2 times anticlock we get str2  and clockwise then str3
so how to check?
```
nirmitnirmit
```
we can see that when we double concatenate the str1 all the rotated one by any degree whether anti or not will be present in it 


```java
class Solution {
    public boolean rotateString(String s, String goal) {
        if(s.length()!=goal.length()){
            return false;
        }
        return (s+s).contains(goal);
    }
}
```

# sorting a string
sorting string is very different and can be done in o(n)
we know 'a'<'b'<'c'<...<'z' if taking lower and same for uppercase also
so count the frequency of each alphabet in the sentence and print them 

```java
class Main {
    public static void main(String[] args) {
        String str="abcdefhshfgesafeywge";
        char[] arr=str.toCharArray();
        int[] res=new int[26];
        for(char i:arr){
            res[i-'a']++;
        }
        String sol="";
        for(int i=0;i<26;i++){
            char temp=(char)('a'+i);
            while(res[i]!=0){
                sol=sol+temp;
                res[i]--;
            }
        }
        System.out.println(sol);
    }
}
```

# integer to roman 
```java
class Solution {
    public String intToRoman(int num) {
        String[] ones={"","I","II","III","IV","V","VI","VII","VIII","IX"};//ALL SINGLE DIGIT
        String[] tens={"","X","XX","XXX","XL","L","LX","LXX","LXXX","XC"};//ALL DOUBLE DIGITS
        String[] huns={"","C","CC","CCC","CD","D","DC","DCC","DCCC","CM"};//ALL TRIPLE DIGITS
        String[] thos={"","M","MM","MMM","MMMM"};//ALL 4 DIGITS
        return thos[num/1000]+huns[(num%1000)/100]+tens[(num%100)/10]+ones[num%10];
    }
}
```
this is very cool one liner 
make array from 0-9, 10-90,100-900,1000-9999 of length 10 each

# factorial of a large number 

```java
import java.util.ArrayList;
import java.util.Collections;
class Main {
    public static void main(String[] args) {
        int num=100;


        ArrayList<Integer> ans=new ArrayList<>();
        ans.add(1);
        while(num>1){
            int carry=0;
            int res=0;
            int size=ans.size();
            for(int i=0;i<size;i++){
                res=ans.get(i)*num+carry;
                carry=res/10;
                ans.set(i,res%10);
            }
            while(carry>0){
                ans.add(carry%10);
                carry/=10;
            }
            // this above loop is used to push digit of carry into the array since one digit at one index
            num--;
        }
        Collections.reverse(ans);
        System.out.println(ans);
        // we use array here instead of string as string is also array of characters so same concept here also
    }
}
```

```
[9, 3, 3, 2, 6, 2, 1, 5, 4, 4, 3, 9, 4, 4, 1, 5, 2, 6, 8, 1, 6, 9, 9, 2, 3, 8, 8, 5, 6, 2, 6, 6, 7, 0, 0, 4, 9, 0, 7, 1, 5, 9, 6, 8, 2, 6, 4, 3, 8, 1, 6, 2, 1, 4, 6, 8, 5, 9, 2, 9, 6, 3, 8, 9, 5, 2, 1, 7, 5, 9, 9, 9, 9, 3, 2, 2, 9, 9, 1, 5, 6, 0, 8, 9, 4, 1, 4, 6, 3, 9, 7, 6, 1, 5, 6, 5, 1, 8, 2, 8, 6, 2, 5, 3, 6, 9, 7, 9, 2, 0, 8, 2, 7, 2, 2, 3, 7, 5, 8, 2, 5, 1, 1, 8, 5, 2, 1, 0, 9, 1, 6, 8, 6, 4, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
```

# sliding window longest substring

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        boolean[] arr=new boolean[256];
        // initially all 0 means no one is touched and 
        // if touched once then 1, after this 
        // if again come then toggle to 0 again 
        int first=0,second=0,len=0;
        while(second<s.length()){
            // this below loop means arr[second] when is 1 and 
            // if come again then enter the loop
            while(arr[s.charAt(second)]){
                arr[s.charAt(first)]=false;
                first++;
            }
            arr[s.charAt(second)]=true;
            len=Math.max(len,second-first+1);
            second++;
        }
        return len;
    }
}
```

# smallest substring with all characters using Sliding Window
```java
class Main {
    public static void main(String[] args) {
        String s="aabbbcbbac";
        int diff=0;
        String temp="";
        for(int i=0;i<s.length();i++){
            if(temp.indexOf(s.charAt(i))==-1){
                diff++;
                temp+=s.charAt(i);
            }
        }// using above we counted the unique letters in the string
        int[] arr=new int[256];
        int first=0,second=0,len=s.length();
        while(second<s.length()){
            while(diff>0 && second<s.length()){
                if(arr[s.charAt(second)]==0){ diff--;}
                arr[s.charAt(second)]++;
                second++;
            }
            len=Math.min(len,second-first);
            while(diff!=1){
                len=Math.min(len,second-first);
                arr[s.charAt(first)]--;
                if(arr[s.charAt(first)]==0){ diff++;}
                first++;
            }
        }
        System.out.println(len);
    }
}
```
