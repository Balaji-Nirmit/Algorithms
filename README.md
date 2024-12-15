# Algorithms
algorithms

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
