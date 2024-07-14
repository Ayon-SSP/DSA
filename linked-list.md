
# 🔗 Linked List
## 1. Singly Linked List
1. **Display** Linked List
2. **Add** at Index in Linked List(first, last, middle, kth)
3. **Remove** at Index in Linked List(first, last, middle, kth)

<details>
<summary>🔽 Code</summary>
<br>
1. Linked List to Stack Adapter && Queue Adapter.

```py
# Definition for singly-linked list.
class ListNode:
    def __init__(self, val = 0, nextNode=None):
        self.val = val
        self.next = nextNode

class LinkedList(object):
    def __init__(self, head=None):
        self.head = head
        self.tail = None
        self.size = 0
    def __repr__(self):
        if self.size == 0:
            return 'None' + "\nSize = " + str(self.size)
        tmp = self.head
        stLinkedList = ""
        while tmp != None:
            stLinkedList += str(tmp.val) + ' -> '
            tmp = tmp.next
        info = f"\nSize = {self.size} Head = {self.head.val} Tail =  {self.tail.val}"
        return stLinkedList + 'None' + info
        
    @classmethod
    def build(cls, lList):
        obj =  cls()
        for ele in lList:
            obj.insertAtTail(ele)
        return obj

    def GetInLst(self):
        lst = []
        tmp = self.head
        while tmp != None:
            lst.append(tmp.val)
            tmp  = tmp.next
        return lst


    def inputLst(self):
        lst = list(map(int,input().split()))
        for ele in lst:
            self.insertAtTail(ele)

    def insertAtHead(self,val):
        newNode = ListNode(val)
        if self.size == 0:
            self.tail = newNode
        else:
            newNode.next = self.head

        self.head = newNode
        self.size += 1
    def insertAtTail(self, val):
        new_node = ListNode(val)
        if self.head == None:
            self.head = self.tail = new_node
        else:
            self.tail.next = new_node
            self.tail = new_node
        self.size += 1
    def insertAtIdx(self,idx,val):
        if not 0 <= idx <= self.size:
            print("Idx out of range")
            return

        newNode = ListNode(val)
        if idx == 0:
            self.insertAtHead(val)
        elif idx == self.size:
            self.insertAtTail(val)
        else:
            tmp = self.head
            for _ in range(idx-1):
                tmp = tmp.next
            newNode.next = tmp.next
            tmp.next = newNode
        self.size += 1

    def deleteAtHead(self):
        if self.size == 0:
            print("Empty Bro!")
            return
        elif self.size == 1:
            self.head = self.tail = None
        else:
            self.head = self.head.next
        self.size -= 1
    def deleteAtTail(self):
        if self.size == 0:
            print("Nothing to remove Bro!")
            return

        if self.size == 1:
            self.head = self.tail = None
        else:
            tmp = self.head
            while tmp.next.next != None:
                tmp = tmp.next
            self.tail = tmp
            tmp.next = None
        self.size -=1
    def deleteAtIdx(self,idx):
        if not 0 <= idx < self.size:
            print("Out of range!")
        elif idx == 0:
            self.deleteAtHead()
        elif idx == self.size - 1:
            self.deleteAtTail()
        else:
            tmp = self.head
            for _ in range(idx-1):
                tmp = tmp.next
            tmp.next = tmp.next.next
            self.size -= 1

    def getHead(self):
        return self.head.val if self.size != 0 else -1
    def getTail(self):
        return self.tail.val if self.size != 0 else -1
    def getAt(self,idx):
        if not 0 <= idx < self.size:
            return "Out of Range!"
        tmp = self.head
        for _ in range(idx):
            tmp = tmp.next
        return "Empty!" if self.size == 0 else tmp.val
    def getAtLastIdx(self,idx):
        # Also you can use recursive
        s = f = self.head
        for _ in range(idx):
            f = f.next
        while f.next != None:
            s = s.next
            f = f.next
        return s
    def getMiddle(self):
        s = f = self.head
        while f.next!=None and f.next.next!=None:
            s = s.next
            f = f.next.next
        return s
    @staticmethod
    def getMiddleWE(hed,tal):
        s = f = hed
        while f.next != tal and f != tal:
            s = s.next
            f = f.next.next
        return s

    # private method
    def __getNodeAt(self,idx):
        if idx >= self.size:
            return "Out of range"
        tmp = self.head
        for _ in range(idx):
            tmp = tmp.next
        return tmp
    def reverseIVals(self):
        li = 0; ri = self.size -1

        while li < ri:
            left = self.__getNodeAt(li)
            right = self.__getNodeAt(ri)
            left.val, right.val = right.val, left.val
            li+=1; ri-=1
    def reverseI(self):
        self.tail = self.head
        pre = None
        curr = self.head
        while curr != None:
            post = curr.next
            curr.next = pre
            pre = curr
            curr = post
        self.head = pre

    # Merge Sort -> merge2SortedLst + merge Function

    # leetcode problem no. 21

    def merge2SortedLst(self,l1, l2):
        tmp1 = l1.head
        tmp2 = l2.head
        res = LinkedList()
        while tmp1 != None and tmp2 != None:
            if tmp1.val < tmp2.val:
                res.insertAtTail(tmp1.val)
                tmp1 = tmp1.next
            else:
                res.insertAtTail(tmp2.val)
                tmp2 = tmp2.next
        while tmp1 != None:
            res.insertAtTail(tmp1.val)
            tmp1 = tmp1.next
        while tmp2 != None:
            res.insertAtTail(tmp2.val)
            tmp2 = tmp2.next
        return res
    def merge(self,hed,tal):
        if hed is tal:
            newLl = LinkedList()
            newLl.insertAtTail(hed.val)
            return newLl
        mid = self.getMiddleWE(hed,tal)
        left = self.merge(hed,mid)
        right = self.merge(mid.next,tal)
        sortedLst = self.merge2SortedLst(left,right)
        return sortedLst


    def mergeSortLst(self):
        llLst = self.merge(self.head,self.tail)
        # self.build(llLst)
        return llLst
        # print(llLst.GetInLst())
        # self.buildnew(llLst.GetInLst())

    # def ww(cls,hed,tal):
    #     return cls.tmpp()
        # if hed == tal:
        #     newL = LinkedList()
        #     newL.insertAtTail(hed.val)
        #     return newL
        # mid = getMiddleWE(hed,tal)


# build
lstLL = [1,2,3,4,5,6,7]
l1 = LinkedList.build(lstLL)
print(l1)

l1 = LinkedList()
l2 = LinkedList()

sz = 9
for ele in range(sz +1):
    l1.insertAtTail(ele)
l1.deleteAtHead()

sorting
4 6 7 17 81 256 777 1000 1001
7 56 70 100 200 250 251 7000
l1.inputLst()
l2.inputLst()
hed = LinkedList.merge2SortedLst
hed = LinkedList.merge2SortedLst(l1,l2)
print(hed)



print(l1.__dict__)
print(l1.__dict__['head'].val)

print(l1.insertAtIdx.__doc__)
help(l1.insertAtIdx)

l1.insertAtHead(55)
l1.insertAtIdx(4,34)
l1.deleteAtTail()
l1.deleteAtIdx(0)
l1.deleteAtTail()
l1.deleteAtIdx(9)
l1.reverseIVals()
print(l1.getAtLastIdx(i).val)
print(l1.getMiddle().val)


print(l1)
print(l2)



mergesort
l1 = LinkedList()
l1.inputLst()
sortedL1 = l1.mergeSortLst()
print(sortedL1)
```
</details>


## 2. Doubly Linked List
1. 2. 3. 🔝
4. **Reverse** Doubly Linked List:
    a. swap the data left -> right ptr1 and right -> left ptr2
    b. swap the node.left and node.right for all nodes.



# [📑 Problems]
> 1. [TUF SDE](https://takeuforward.org/linked-list/top-linkedlist-interview-questions-structured-path-with-video-solutions) + [Pepcoding](https://www.youtube.com/playlist?list=PL-Jc9J83PIiF5VZmktfqW6WVU1pxBF6l_) + Leetcode + NeetCode + Youtube.
### 707. Design Linked List: [🪖 Leetcode](https://leetcode.com/problems/design-linked-list/)
```py
class ListNode:
    def __init__(self, val=0, next=None, prev=None):
        self.val = val
        self.next = next
        self.prev = prev

class MyLinkedList:

    def __init__(self):
        self.head = None
        self.tail = None
        self.size = 0

    def get(self, index: int) -> int:
        if not self.head or not index < self.size:
            return -1
        cur = self.head
        for _ in range(index):
            cur = cur.next
        return cur.val


    def addAtHead(self, val: int) -> None:
        if not self.size:
            self.head = self.tail = ListNode(val)
        else:
            self.head.prev = ListNode(val, self.head, None)
            self.head = self.head.prev
        self.size += 1

    def addAtTail(self, val: int) -> None:
        if not self.size:
            self.tail = self.head = ListNode(val)
        else:
            self.tail.next = ListNode(val, None, self.tail)
            self.tail = self.tail.next
        self.size += 1

    def addAtIndex(self, index: int, val: int) -> None:
        if index < 0 or self.size < index:
            return
        if index == 0:
            self.addAtHead(val)
        elif index == self.size:
            self.addAtTail(val)
        else:
            cur = self.head
            for _ in range(index -1):
                cur = cur.next
            node = ListNode(val, cur.next, cur)
            cur.next = node
            cur.next.next.prev = node
            self.size += 1

    def deleteAtIndex(self, index: int) -> None:
        if index < 0 or self.size <= index:
            return

        if index == 0:
            self.head = self.head.next
            if self.size == 1:
                self.tail = self.tail.prev
            else:
                self.head.prev = None
        elif index == self.size -1:
            self.tail = self.tail.prev
            self.tail.next = None
        else:
            cur = self.head
            for _ in range(index -1):
                cur = cur.next
            cur.next = cur.next.next
            cur.next.prev = cur
        self.size -= 1

    def display(self):
        print(self.head.val, self.tail.val, self.size)
        cur = self.head
        curBack = self.tail
        print(self.size)
        while cur:
            print(f"| {cur.prev.val if cur.prev else 'None':4} | {cur.val:4} | {cur.next.val if cur.next else 'None':4}")
            cur = cur.next
        print()
        while curBack:
            print(f"| {curBack.prev.val if curBack.prev else 'None':4} | {curBack.val:4} | {curBack.next.val if curBack.next else 'None':4}")
            curBack = curBack.prev
        print()
        


# Your MyLinkedList object will be instantiated and called as such:
# obj = MyLinkedList()
# param_1 = obj.get(index)
# obj.addAtHead(val)
# obj.addAtTail(val)
# obj.addAtIndex(index,val)
# obj.deleteAtIndex(index)
```
### 206. Reverse Linked List: [🪖 Leetcode](https://leetcode.com/problems/reverse-linked-list/)
```py
"""
1. using stack
    Can use a Stack storing all the node ptr
    poping iteratively and updatng the node.next = stack.top .... 
2. Using 2 pointers:
    left and right ptr
3. using recursive right -> left
4. using iter left -> right
"""
# Definition for singly-linked list.
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        # T: O(N) M: O(1)
        prev, curr = None, head

        while curr:
            # storing next ptr for next iteration
            nxt = curr.next

            # # reversing the pointer
            # # prev curr->nxt->nxt.nxt... to prev<-curr nxt->nxt.nex... 
            curr.next = prev

            # # Updating the points
            prev = curr
            curr = nxt

        return prev
```
#### ♻️ Using Recursion
```py
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        # Recursive -> T: O(N) M: O(N)
        if not head or not head.next:
            return head

        newHead = self.reverseList(head.next)
        head.next.next = head
        head.next = None

        return newHead
```
#### ⚓ Using Iteration
```py
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        last = None
        while head:
            """3,1,2 = 1,2,3"""
            head.next, last, head = last, head, head.next     
        return last
```
### 876. Middle of the Linked List: [🪖 Leetcode](https://leetcode.com/problems/middle-of-the-linked-list/)
```py
# Definition for singly-linked list.
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def middleNode(self, head: Optional[ListNode]) -> Optional[ListNode]:
        slow, fast = head, head
        while fast and fast.next:
            slow, fast = slow.next, fast.next.next
        return slow
```
### 19. Remove Nth Node From End of List: [🪖 Leetcode](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)
> or get Kth node from the end
> 1. Using 2 pointers: 
>   - Move the fast ptr `k` steps ahead
>   - Move both slow and fast ptr until fast reaches the end

```py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        dummy = ListNode()
        dummy.next = head
        
        first, second = dummy, dummy
        for _ in range(n+1):
            second = second.next
        
        while second:
            first, second = first.next, second.next
        
        # remove first.next
        first.next = first.next.next
        return dummy.next
```
### 234. Palindrome Linked List: [🪖 Leetcode](https://leetcode.com/problems/palindrome-linked-list/)
```py
# Definition for singly-linked list.
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next
class Solution:
    def middleNode(self, head: Optional[ListNode]) -> Optional[ListNode]:
        slow, fast = head, head
        while fast and fast.next:
            slow, fast = slow.next, fast.next.next
        return slow

    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        last = None
        while head:
            head.next, last, head = last, head, head.next
        return last

    def isPalindrome(self, head: Optional[ListNode]) -> bool:
        midNode = self.middleNode(head)
        newLL = self.reverseList(midNode)
        while newLL:
            if head.val != newLL.val:
                return False
            head, newLL = head.next, newLL.next
        return True
```
### 237. Delete Node in a Linked List: [🪖 Leetcode](https://leetcode.com/problems/delete-node-in-a-linked-list/)
```py
class Solution:
    def deleteNode(self, node):
        """ T: O(1) M: O(1)"""
        """
        :type node: ListNode
        :rtype: void Do not return anything, modify node in-place instead.
        """
        # assigne the next val to curr val and delete the next node
        node.val = node.next.val
        node.next = node.next.next
```
### 2. Add Two Numbers: [🪖 Leetcode](https://leetcode.com/problems/add-two-numbers/)
```py
# Definition for singly-linked list.
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        head, cry = ListNode(), 0
        dummy = head

        while l1 or l2 or cry:
            # Calculating the cry and curSum
            cur_sum = (l1.val if l1 else 0) + (l2.val if l2 else 0) + cry
            cry, cur_sum = divmod(cur_sum,10)

            # Adding new Node at the end with cur_sum
            head.next = ListNode(cur_sum)

            # Updating ptr's
            head = head.next
            l1, l2 = l1.next if l1 else None, l2.next if l2 else None

        return dummy.next
```
### 21. Merge Two Sorted Lists: [🪖 Leetcode](https://leetcode.com/problems/merge-two-sorted-lists/)
```py
# Definition for singly-linked list.
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next
        
class Solution:
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        dummy = ListNode()
        curNode = dummy

        while list1 and list2:
            if list1.val < list2.val:
                nodeAL = list1
                list1 = list1.next
            else:
                nodeAL = list2
                list2 = list2.next

            nodeAL.next = None
            curNode.next = nodeAL
            curNode = curNode.next
        
        curNode.next = list1 if list1 else list2
        return dummy.next  
```
### 148. Sort List: [🪖 Leetcode](https://leetcode.com/problems/sort-list/)
```py
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        dummy = ListNode()
        curNode = dummy
        while list1 and list2:
            if list1.val <= list2.val:
                nodeTA = list1
                list1 = list1.next
            else:
                nodeTA = list2
                list2 = list2.next

            nodeTA.next = None
            curNode.next = nodeTA
            curNode = curNode.next
        
        curNode.next = list1 if list1 else list2
        return dummy.next

    def middleNode(self, head: Optional[ListNode]) -> Optional[ListNode]:
        slow, fast = head, head
        while fast and fast.next and fast.next.next:
            slow, fast = slow.next, fast.next.next
        return slow
    
    def sortList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if not head:
            return None
        if not head.next:
            return head
        
        # Divide the LL, break ptr
        mid = self.middleNode(head)
        left, right = head, mid.next
        mid.next = None

        # merge 2 sorted
        newLeft = self.sortList(left)
        newRight = self.sortList(right)
        newHead = self.mergeTwoLists(newLeft, newRight)
        return newHead
```
### sort 0 1 | odd even: using pointers [📺 Video](https://youtu.be/gRII7LhdJWc?si=A16rwfJmUpUB56AH)
### 328. Odd Even Linked List: [🪖 Leetcode](https://leetcode.com/problems/odd-even-linked-list/)
### 160. Intersection of Two Linked Lists: [🪖 Leetcode](https://leetcode.com/problems/intersection-of-two-linked-lists/)
```py
# Definition for singly-linked list.
class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None
"""
Find intersection point of Y LinkedList:
0. Using Hashmap time O(m + n) space O(n)
1. find both the length as m and n diff = abs(m-n) traves parallely O(n + m) big code
2. 2 dummy nodes each travling both the linked list at some point they will meet O(n + m)
"""
class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> Optional[ListNode]:
        a, b = headA, headB
        while a != b:
            a = a.next if a else headB
            b = b.next if b else headA
        return a
```
### 141. Linked List Cycle(Floyd's Tortoise): [🪖 Leetcode](https://leetcode.com/problems/linked-list-cycle/) [`📺 Best Explanation`](https://youtu.be/gBTe7lFR3vc?t=351)
```py
"""
1. You can use the hashmap(dictionary) store all the elements if it's repeates then True else false.
2. Can use slow and fast pointer
"""
# Definition for singly-linked list.
class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None

class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        """ T: O(N) M: O(1) """
        s, f = head, head
        while f and f.next:
            s, f = s.next, f.next.next
            if s == f:
                return True
        return False
```
### 142. Linked List Cycle II: [🪖 Leetcode](https://leetcode.com/problems/linked-list-cycle-ii/) [📺 Exp](https://youtu.be/2Kd0KKmmHFc?list=PLgUwDviBIf0rAuz8tVcM0AymmhTRsfaLU&t=942)
```py
# Definition for singly-linked list.
class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None

class Solution:
    def detectCycle(self, head: Optional[ListNode]) -> Optional[ListNode]:
        s, f = head, head
        while f and f.next:
            s, f = s.next, f.next.next
            if s == f:
                break
        else:
            return None
        
        nptr = head
        while nptr != s:
            s, nptr = s.next, nptr.next
        
        return nptr
```
### L15. Find the length of the Loop in LinkedList [📺 Video](https://youtu.be/I4g1qbkTPus?si=K3TshZ4yfgAI3cmc)
> 1. Using Hashmap
> 2. Using Floyd's Tortoise: first find the cycle then find the length of the cycle.
### L11. Add 1 to a number represented by LinkedList: [🪖 Leetcode](https://leetcode.com/problems/plus-one-linked-list/) [📺 Video](https://youtu.be/aXQWhbvT3w0?si=h8dkIn-BD80JBhvN)
> 159 + 1 -> 160 | 999 + 1 -> 1000
> - Reverse the linked list and add 1 and reverse it again
> - Using recurssion
```py
# Definition for singly-linked list.
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def plusOne(self, head: Optional[ListNode]) -> Optional[ListNode]:
        def addOne(node):
            if not node:
                return 1
            carry = addOne(node.next)
            if carry:
                node.val += carry
                carry = node.val // 10
                node.val %= 10
            return carry

        carry = addOne(head)
        if carry:
            return ListNode(1, head)
        return head
```
### L19. Find all Pairs with given Sum in DLL
> Using 2 pointers left and right
### 61. Rotate List: [🪖 Leetcode](https://leetcode.com/problems/rotate-list/)
```py
"""
k = 2
1 2 3 4 5 6 7
s   f
H       s   f
   None   H  H.next
"""
# Definition for singly-linked list.
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def lengthList(self, head: Optional[ListNode]) -> int:
        cnt = 0
        while head:
            head = head.next
            cnt += 1
        return cnt

    def rotateRight(self, head: Optional[ListNode], k: int) -> Optional[ListNode]:
        if not head:
            return head

        k = k % self.lengthList(head)

        if not k:
            return head

        first, second = head, head

        for _ in range(k):
            second = second.next
        
        while second.next:
            first, second = first.next, second.next

        second.next = head
        head = first.next
        first.next = None

        return head 
```
### L24. Flattening a LinkedList: [🥷 Coding Ninjas](https://www.naukri.com/code360/problems/flatten-a-linked-list_1112655)
```
    5 -> 10 -> 19 -> 28     5 -> 10 -> 19           
    |    |     |     |      |    |     |            
    V    V     V     V      V    V     V            
    7    20    22    35     7    20    22           
    |          |     |   -> |          |            
    V          V     V      V          V      -> ...
    8          50    40     8          28           
    |                |      |          |            
    V                V      V          V            
    30               45     30         35 
                                       |
                                       V
                                       40
                                       45
                                       50 
1. merge last 2 LL recursively.
```
```py
"""
    Time Complexity: O(n * n * k)
    Space complexity: O(n * k)

    Where 'n' denotes the size of the linked list and 'k' is the average number of child nodes for each of the n nodes.
"""

class Node:
    def __init__(self, val=0, next=None, child=None):
        self.data = val
        self.next = next
        self.child = child

def merge(first: Node, second: Node) -> Node:
    if not first:
        second.next = None
        return second

    if not second:
        first.next = None
        return first

    merged = None

    if first.data < second.data:
        merged = first
        merged.child = merge(first.child, second)
    else:
        merged = second
        merged.child = merge(first, second.child)
    merged.next = None
    return merged


def flattenLinkedList(head: Node) -> Node:
    if not head or not head.next:
        return head

    head.next = flattenLinkedList(head.next)

    head = merge(head, head.next)
    return head
```
### 138. Copy List with Random Pointer: [🪖 Leetcode](https://leetcode.com/problems/copy-list-with-random-pointer/)
```py
# Definition for a Node.
class Node:
    def __init__(self, x: int, next: 'Node' = None, random: 'Node' = None):
        self.val = int(x)
        self.next = next
        self.random = random

class Solution:
    def copyRandomList(self, head: 'Optional[Node]') -> 'Optional[Node]':
        oldToCopy = {None : None}

        cur = head
        while cur:
            copy = Node(cur.val)
            oldToCopy[cur] = copy
            cur = cur.next
        
        cur = head
        while cur:
            copy = oldToCopy[cur]
            copy.next = oldToCopy[cur.next]
            copy.random = oldToCopy[cur.random]
            cur = cur.next
        
        return oldToCopy[head]
```
### 25. Reverse Nodes in k-Group: [🪖 Leetcode](https://leetcode.com/problems/reverse-nodes-in-k-group/)
```py
"""
Let k = 5
                           prev  curr --> in the last Iter of reverse loop 
dummy -> 1 -> 2 -> 3 -> 4 -> 5 -> 6 -> 7
grpPrev                     kth  grpNxt    

dummy -> 5 -> 4 -> 3 -> 2 -> 1 -> 6 -> 7
                          grpPrev            kth   grpNxt    
"""

class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def getKth(self, cur, k):
        while cur and  k > 0:
            cur = cur.next
            k -= 1
        return cur

    def reverseKGroup(self, head: Optional[ListNode], k: int) -> Optional[ListNode]:
        dummy = ListNode(0, head)
        groupPrev = dummy

        while True:
            kth = self.getKth(groupPrev, k)
            if not kth:
                break
            groupNext = kth.next

            prev, curr = kth.next, groupPrev.next
            while curr != groupNext:
                # storing for future use
                nxt = curr.next

                # pointing to the prev ptr
                curr.next = prev

                # updating the ptr's
                prev = curr
                curr = nxt
            
            tmp = groupPrev.next
            groupPrev.next = kth
            groupPrev = tmp
        
        return dummy.next
```
### 143. Reorder List: [🪖 Leetcode](https://leetcode.com/problems/reorder-list/)
```py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseLinkedList(self, head):
        prev, curr = None, head
        while curr:
            nxt = curr.next
            curr.next = prev
            prev = curr
            curr = nxt
        return prev

    def reorderList(self, head: Optional[ListNode]) -> None:
        s,f = head, head
        while f and f.next:
            s,f = s.next, f.next.next
        """
        p1 -> 1 2 3 4 5
        p2 -> 6 7 8 9 10
        """
        p1 = head
        p2 = self.reverseLinkedList(s)
        
        while p2.next:
            # Saving the points
            nxt1 = p1.next
            nxt2 = p2.next
            
            # 
            p1.next = p2
            p2.next = nxt1
            
            # updating the points
            p1 = nxt1
            p2 = nxt2
```
### 86. Partition List: [🪖 Leetcode](https://leetcode.com/problems/partition-list/)
```py
# Definition for singly-linked list.
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next
class Solution:
    def partition(self, head: Optional[ListNode], x: int) -> Optional[ListNode]:
        left, right = ListNode(), ListNode()
        ltail, rtail = left, right

        while head:
            if head.val < x:
                ltail.next = head
                ltail = ltail.next
            else:
                rtail.next = head
                rtail = rtail.next
            head = head.next
        
        ltail.next = right.next
        rtail.next = None

        return left.next
```



TODO: All below problems.
```py
# ---------------------------<doubLL>-----------------------------
# /Rand Cache
"""
class Node:
    def __init__(self, key, value):
        self.key, self.val = key, value
        self.prev = self.next = None


class LRUCache:

    def __init__(self, capacity: int):
        self.cap = capacity
        self.cache = {} #map key to node

        # left -> LRU & right -> MRU
        self.left, self.right = Node(0, 0), Node(0, 0)
        self.left.next, self.right.prev = self.right, self.left


    def get(self, key: int) -> int:
        if key in self.cache:
            return self.cache[key].val
        else: return -1

    def put(self, key: int, value: int) -> None:
        if not len(self.cache) < self.cap:

            # Deleting Node
            n1, n2, n3 = self.left, self.left.next, self.left.next.next
            print(n1.val,n2.val,n3.val)
            n1.next,n3.prev = n3, n1

            # Deliting from cache
            del self.cache[n2.key]

        if key not in self.cache:
            # Node Inserting
            curNode = Node(key, value)
            curNode.prev, curNode.next = self.right.prev,self.right
            self.right.prev.next = curNode
            self.right.prev = curNode

            # Adding in Cach
            self.cache[key] = curNode

        elif key in self.cache:
            self.cache[key].val = value

    def pp(self):

        print("------*-------*-----*-----*-------*-------*-----*-----*-------*-------*-")
        print(self.cache)
        print("------------------------")
        temp = self.left
        for _ in range(len(self.cache) + 2):
            print(temp.val,end="->")
            temp = temp.next
        print()
        print("------------------")
        temp = self.right
        for _ in range(len(self.cache) + 2):
            print(temp.val,end="->")
            temp = temp.prev
        print()


# Your LRUCache object will be instantiated and called as such:
obj = LRUCache(2)
obj.put(1,1)
obj.put(2,2)
obj.get(1)
obj.
# obj.put(20, 20)
# obj.put(8,8)
# obj.put(3,6)
# obj.put(12,6)
# obj.put(1456,43)
param_1 = obj.get(20)
print(param_1)

obj.pp()

"""

# /146. LRU Cache
"""
class Node:
    def __init__(self, key, value):
        self.key, self.val = key, value
        self.prev = self.next = None


class LRUCache:

    def __init__(self, capacity: int):
        self.cap = capacity
        self.cache = {}  # map key to node

        # left -> LRU & right -> MRU
        self.left, self.right = Node(0, 0), Node(0, 0)
        self.left.next, self.right.prev = self.right, self.left

        # remove node from list

    def removeAt(self, node):
        prev, nxt = node.prev, node.next
        prev.next, nxt.prev = nxt, prev

    # insert node at right
    def insertAt(self, node):
        prev, nxt = self.right.prev, self.right
        prev.next = nxt.prev = node
        node.next, node.prev = nxt, prev

    def get(self, key: int) -> int:
        if key in self.cache:
            self.removeAt(self.cache[key])
            self.insertAt(self.cache[key])
            return self.cache[key].val
        return -1

    def put(self, key: int, value: int) -> None:
        if key in self.cache:
            self.removeAt(self.cache[key])
        self.cache[key] = Node(key, value)
        self.insertAt(self.cache[key])

        if len(self.cache) > self.cap:
            # remove from the list and delete the LRU from the hashmap
            lru = self.left.next
            self.removeAt(lru)
            del self.cache[lru.key]


# Your LRUCache object will be instantiated and called as such:
# obj = LRUCache(capacity)
# param_1 = obj.get(key)
# obj.put(key,value)
"""
# /460. LFU Cache
"""
class ListNode:
    def __init__(self,key , val, prev = None, next = None):
        self.key, self.val = key, val
        self.prev, self.next  = prev, next
class LinkedList:
    def __init__(self):
        self.map = {}
        self.left, self.right = ListNode(0,0), ListNode(0,0)
        self.left.next, self.right.prev = self.right, self.left


    def length(self):
        return len(self.map)

    def pushRight(self, val):
        node = ListNode(val, self.right.prev, self.right)
        self.map[val] = node
        self.right.prev = node.prev.next = node

    def pop(self, val):
        if val in self.map:
            node = self.map[val]
            prev, next = node.prev, node.next
            prev.next = next
            next.prev = prev
            self.map.pop(val,None)

    def popLeft(self):
        res = self.left.next.val
        self.pop(self.left.next.val)
        return res

    def update(self, val):
        self.pop(val)
        self.pushRight(val)


class LFUCache:

    def __init__(self, capacity: int):
        self.cap = capacity
        self.lfucnt = 0 # Map key -> val
        self.valMap = {}
        self.countMap = collections.defaultdict(int)
        # Map count of key -> linkedlsit
        self.listMap = collections.defaultdict(LinkedList)

    def counter(self, key):
        cnt = self.countMap[key]
        self.countMap[key] += 1
        self.listMap[cnt].pop(key)
        self.listMap[cnt + 1].pushRight(key)

        if cnt == self.lfucnt and self.listMap[cnt].length() == 0:
            self.lfucnt += 1


    def get(self, key: int) -> int:
        if key not in self.valMap:
            return -1
        self.counter(key)
        return self.valMap[key]

    def put(self, key: int, value: int) -> None:
        if self.cap == 0:
            return
        if key not in self.valMap and len(self.valMap) == self.cap:
            res = self.listMap[self.lfucnt].popLeft()
            self.valMap.pop(res)
            self.countMap.pop(res)

        self.valMap[key] = value
        self.counter(key)
        self.lfucnt = min(self.lfucnt, self.countMap[key])

# Your LFUCache object will be instantiated and called as such:
# obj = LFUCache(capacity)
# param_1 = obj.get(key)
# obj.put(key,value)
"""
```











# 🕜 LinkedList Old Code

<details>
<summary><h3>🪗 Code 🪗</h3></summary>

```py
# @Rand---------------------------<LinkedList>-----------------------------
# Learned from Striver: https://www.youtube.com/playlist?list=PLgUwDviBIf0r47RKH7fdWN54AbWFgGuii


# /160. Intersection of Two Linked Lists
"""
0. Using Hashmap time O(m + n) space O(n)
1. find both the length as m and n diff = abs(m-n) traves parallely O(n + m) big code
2. 2 dummy nodes each travling both the linked list at some point they will meet O(n + m)
"""
"""
class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> Optional[ListNode]:
        a, b = headA, headB
        while a != b:
            a = a.next if a else headB
            b = b.next if b else headA

        return a
"""
# /141. Linked List Cycle
"""
1. You can use the hashmap(dictionary) store all the elements if it's repeates then True else false.
2. Can use slow and fast pointer
"""
"""
class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None

class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        s, f = head, head
        while f and f.next:
            s, f = s.next, f.next.next
            if s == f:
                return True
        return False
"""
# /25. Reverse Nodes in k-Group
"""
Let k = 5
                           prev  curr --> in the last Iter of reverse loop 
dummy -> 1 -> 2 -> 3 -> 4 -> 5 -> 6 -> 7
grpPrev                     kth  grpNxt    

dummy -> 5 -> 4 -> 3 -> 2 -> 1 -> 6 -> 7
                          grpPrev                    kth   grpNxt    
"""
"""
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def getKth(self, cur, k):
        while cur and k > 0:
            cur = cur.next
            k -= 1
        return cur

    def reverseKGroup(self, head: Optional[ListNode], k: int) -> Optional[ListNode]:
        dummy = ListNode(0, head)
        groupPrev = dummy

        while True:
            kth = self.getKth(groupPrev, k)
            if not kth:
                break
            groupNext = kth.next

            prev, curr = kth.next, groupPrev.next
            while curr != groupNext:
                # storing for future use
                nxt = curr.next

                # pointing to the prev ptr
                curr.next = prev

                # updating the ptr's
                prev = curr
                curr = nxt

            tmp = groupPrev.next
            groupPrev.next = kth
            groupPrev = tmp

        return dummy.next
"""
# /61. Rotate List
"""
k = 2
1 2 3 4 5 6 7
s   f
H       s   f
   None   H  H.next

k = 1
1 -> None
s    f
"""
"""
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def lengthList(self, head: Optional[ListNode]) -> int:
        cnt = 0
        cur = head
        while cur:
            cur = cur.next
            cnt += 1
        return cnt

    def rotateRight(self, head: Optional[ListNode], k: int) -> Optional[ListNode]:
        if not head:
            return head

        length = self.lengthList(head)
        k = k % length

        if k == 0:
            return head

        s, f = head, head
        for _ in range(k):
            f = f.next

        while f and f.next:
            s, f = s.next, f.next

        head, f.next, s.next = s.next, head, None
        return head
"""
# /21. Merge Two Sorted Lists
"""
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next
class Solution:
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        dummy = ListNode()
        curNode = dummy
        while list1 and list2:
            if list1.val <= list2.val:
                nodeTA = list1
                list1 = list1.next
            else:
                nodeTA = list2
                list2 = list2.next

            nodeTA.next = None
            curNode.next = nodeTA
            curNode = curNode.next
        
        curNode.next = list1 if list1 else list2
        return dummy.next
"""

# 143. Reorder List
# Definition for singly-linked list.
"""
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseLinkedList(self, head):
        prev, curr = None, head
        while curr:
            nxt = curr.next
            curr.next = prev
            prev = curr
            curr = nxt
        return prev

    def reorderList(self, head: Optional[ListNode]) -> None:
        s, f = head, head
        while f and f.next:
            s, f = s.next, f.next.next

        # p1 -> 1 2 3 4 5
        # p2 -> 6 7 8 9 10
        
        p1 = head
        p2 = self.reverseLinkedList(s)

        while p2.next:
            # Saving the points
            nxt1 = p1.next
            nxt2 = p2.next

            # 
            p1.next = p2
            p2.next = nxt1

            # updating the points
            p1 = nxt1
            p2 = nxt2
"""
# ---------------------------<doubLL>-----------------------------
# /Rand Cache
"""
class Node:
    def __init__(self, key, value):
        self.key, self.val = key, value
        self.prev = self.next = None


class LRUCache:

    def __init__(self, capacity: int):
        self.cap = capacity
        self.cache = {} #map key to node

        # left -> LRU & right -> MRU
        self.left, self.right = Node(0, 0), Node(0, 0)
        self.left.next, self.right.prev = self.right, self.left


    def get(self, key: int) -> int:
        if key in self.cache:
            return self.cache[key].val
        else: return -1

    def put(self, key: int, value: int) -> None:
        if not len(self.cache) < self.cap:

            # Deleting Node
            n1, n2, n3 = self.left, self.left.next, self.left.next.next
            print(n1.val,n2.val,n3.val)
            n1.next,n3.prev = n3, n1

            # Deliting from cache
            del self.cache[n2.key]

        if key not in self.cache:
            # Node Inserting
            curNode = Node(key, value)
            curNode.prev, curNode.next = self.right.prev,self.right
            self.right.prev.next = curNode
            self.right.prev = curNode

            # Adding in Cach
            self.cache[key] = curNode

        elif key in self.cache:
            self.cache[key].val = value

    def pp(self):

        print("------*-------*-----*-----*-------*-------*-----*-----*-------*-------*-")
        print(self.cache)
        print("------------------------")
        temp = self.left
        for _ in range(len(self.cache) + 2):
            print(temp.val,end="->")
            temp = temp.next
        print()
        print("------------------")
        temp = self.right
        for _ in range(len(self.cache) + 2):
            print(temp.val,end="->")
            temp = temp.prev
        print()


# Your LRUCache object will be instantiated and called as such:
obj = LRUCache(2)
obj.put(1,1)
obj.put(2,2)
obj.get(1)
obj.
# obj.put(20, 20)
# obj.put(8,8)
# obj.put(3,6)
# obj.put(12,6)
# obj.put(1456,43)
param_1 = obj.get(20)
print(param_1)

obj.pp()

"""

# /146. LRU Cache
"""
class Node:
    def __init__(self, key, value):
        self.key, self.val = key, value
        self.prev = self.next = None


class LRUCache:

    def __init__(self, capacity: int):
        self.cap = capacity
        self.cache = {}  # map key to node

        # left -> LRU & right -> MRU
        self.left, self.right = Node(0, 0), Node(0, 0)
        self.left.next, self.right.prev = self.right, self.left

        # remove node from list

    def removeAt(self, node):
        prev, nxt = node.prev, node.next
        prev.next, nxt.prev = nxt, prev

    # insert node at right
    def insertAt(self, node):
        prev, nxt = self.right.prev, self.right
        prev.next = nxt.prev = node
        node.next, node.prev = nxt, prev

    def get(self, key: int) -> int:
        if key in self.cache:
            self.removeAt(self.cache[key])
            self.insertAt(self.cache[key])
            return self.cache[key].val
        return -1

    def put(self, key: int, value: int) -> None:
        if key in self.cache:
            self.removeAt(self.cache[key])
        self.cache[key] = Node(key, value)
        self.insertAt(self.cache[key])

        if len(self.cache) > self.cap:
            # remove from the list and delete the LRU from the hashmap
            lru = self.left.next
            self.removeAt(lru)
            del self.cache[lru.key]


# Your LRUCache object will be instantiated and called as such:
# obj = LRUCache(capacity)
# param_1 = obj.get(key)
# obj.put(key,value)
"""
# /460. LFU Cache
"""
class ListNode:
    def __init__(self,key , val, prev = None, next = None):
        self.key, self.val = key, val
        self.prev, self.next  = prev, next
class LinkedList:
    def __init__(self):
        self.map = {}
        self.left, self.right = ListNode(0,0), ListNode(0,0)
        self.left.next, self.right.prev = self.right, self.left


    def length(self):
        return len(self.map)

    def pushRight(self, val):
        node = ListNode(val, self.right.prev, self.right)
        self.map[val] = node
        self.right.prev = node.prev.next = node

    def pop(self, val):
        if val in self.map:
            node = self.map[val]
            prev, next = node.prev, node.next
            prev.next = next
            next.prev = prev
            self.map.pop(val,None)

    def popLeft(self):
        res = self.left.next.val
        self.pop(self.left.next.val)
        return res

    def update(self, val):
        self.pop(val)
        self.pushRight(val)


class LFUCache:

    def __init__(self, capacity: int):
        self.cap = capacity
        self.lfucnt = 0 # Map key -> val
        self.valMap = {}
        self.countMap = collections.defaultdict(int)
        # Map count of key -> linkedlsit
        self.listMap = collections.defaultdict(LinkedList)

    def counter(self, key):
        cnt = self.countMap[key]
        self.countMap[key] += 1
        self.listMap[cnt].pop(key)
        self.listMap[cnt + 1].pushRight(key)

        if cnt == self.lfucnt and self.listMap[cnt].length() == 0:
            self.lfucnt += 1


    def get(self, key: int) -> int:
        if key not in self.valMap:
            return -1
        self.counter(key)
        return self.valMap[key]

    def put(self, key: int, value: int) -> None:
        if self.cap == 0:
            return
        if key not in self.valMap and len(self.valMap) == self.cap:
            res = self.listMap[self.lfucnt].popLeft()
            self.valMap.pop(res)
            self.countMap.pop(res)

        self.valMap[key] = value
        self.counter(key)
        self.lfucnt = min(self.lfucnt, self.countMap[key])

# Your LFUCache object will be instantiated and called as such:
# obj = LFUCache(capacity)
# param_1 = obj.get(key)
# obj.put(key,value)
"""

# endOf -<LinkedList>->

```

</details>