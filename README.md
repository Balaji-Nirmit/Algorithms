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
