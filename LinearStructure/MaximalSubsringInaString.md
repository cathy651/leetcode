Maximal Subsring In a String


```java 
class Solution {
  public static void main(String[] args) {
    
    String str1 = "My name is Jason";
                                    
    // System.out.println(xxxx(str1)); // log: Jason
    String sens = "you and me";
                      // r
                   // l
    
    System.out.println(longestWord(sens)); // log: Jason
  }

  // 方法一： string array , time: n, space n 


    public static String longestWord(String sens){
    String res = "";
    String[] resArr = sens.split(" ");
    
    for(int i = 0; i < resArr.length; i++){
      if(resArr[i].length() > res.length()){
        res = resArr[i];
      }
    }
    return res;
  }
  
  // 方法二 two pointer , time : n , space 1
  
  public static String longestWord(String sens) {
    int l = -1, r = 0;
    
    String res = "";
      
    while(r < sens.length()){
      if(sens.charAt(r) == ' ') {
        String tmp = sens.substring(l + 1, r);
        // check if need to update res
        if(tmp.length() > res.length()){
          res = tmp;
        }
        // update l
        l = r; 
      }
      r++;
    }
    
    // r == sens.length();
    // l == last space
    String last = sens.substring(l, r);
    if(last.length() > res.length()){
      res = last;
    }
    
    return res;
  }
}

```
