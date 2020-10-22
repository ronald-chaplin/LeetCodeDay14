## Add Two Numbers II

```
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        Stack<Integer> s1 = new Stack<>();
        Stack<Integer> s2 = new Stack<>();
        
        while(l1 != null){
            s1.push(l1.val);
            l1 = l1.next;
        }
        while(l2 != null){
            s2.push(l2.val);
            l2 = l2.next;
        }
        
        System.out.println(s1);
        System.out.println(s2);
        
        ListNode temp = new ListNode(0);
        int carry = 0;
        while(!s1.isEmpty() || !s2.isEmpty() || carry == 1){
            int v1 = s1.isEmpty() ? 0 : s1.pop();
            int v2 = s2.isEmpty() ? 0 : s2.pop();
            int sum = v1 + v2 + carry;
            carry = sum >= 10 ? 1 : 0;
            ListNode node = new ListNode(sum % 10);
            node.next = temp.next;
            temp.next = node;
        }
        
        return temp.next;
    }
}

```

## Decode String

```
class Solution {
    public String decodeString(String s) {
        if (s.length() == 0 || s == null) {
            return s;
        }
        Stack<String> strStack = new Stack<String>();
        Stack<Integer> numStack = new Stack<Integer>();
        StringBuilder decoded = new StringBuilder();
        int x = 0;
        while (x < s.length()) {
            if (Character.isDigit(s.charAt(x))) {
                int num = 0;
                while (Character.isDigit(s.charAt(x))) {
                    num = num * 10 + (s.charAt(x) - '0');
                    x++;
                }
                numStack.push(num);
            } else if (s.charAt(x) == '[') {
                strStack.push(decoded.toString());
                decoded = new StringBuilder("");
                x++;
            } else if (s.charAt(x) == ']') {
                StringBuilder sequence = new
                StringBuilder(strStack.pop());
                int times = numStack.pop();
                for (int i = 0; i < times; i++) {
                    sequence.append(decoded);
                }
                decoded = sequence;
                x++;
            } else {
                decoded.append(s.charAt(x++));
            }
        }
        return decoded.toString();
    }
}
```
