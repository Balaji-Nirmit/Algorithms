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
