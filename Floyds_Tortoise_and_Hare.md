[环判断]



**问题**

给定一个链表，返回环路开始节点，如果没有则返回空。



**直觉**

当一个跑得快的跑步者和一个跑得慢的跑步者在有环形的跑道上赛跑会发生什么？在某个时刻，快的跑步者将追上慢的跑步者。

**算法**

Floyd算法分为两个不同的阶段。第一个阶段是判断在链表中是否有环路，如果不存在就马上返回空，也就不存在第二阶段。第二个阶段就是找到环路的入口。

第一阶段

在这里，我们初始化两个指针-快的hare和慢的tortoise。接下来，hare和tortoise从同一个节点出发（头节点），tortoise每次走一个节点，hare每次走两个节点。如果他们在前进若干步后在同一个节点相遇，我们就返回这个节点，如果最终没有返回节点信息，而是返回空，则代表不存在环路。

证明如图

![img](http://write.blog.csdn.net/postedit/78761940)![img](https://leetcode.com/articles/Figures/142/Slide1.PNG)

这里，设环的长度为*C* ,非环部分的长度为*F*，当tortoise指针第一次到达0节点（环入口）的时候,hare指针指向*h*节点，其中*F*≡*h*(mod*C*)。由于hare的速度为tortoise的两倍，所以hare的路程为 2*F*，即在环中走了*F*  的路程，正好 *F* 和 *h* 对于模 *C* 同余。接下来hare离入口节点的距离为*C*−*h*, 那么当tortoise再走 *C*−*h* 的路程时，hare正好走了2(*C*−*h*) 的路程，而此刻他们都在*C*−*h*相遇。



h+2(C−h)=2C−h≡C−h(modC)h+2(C−h)=2C−h≡C−h(modC)



第二阶段

由于第一阶段确定了有环路，第二阶段就是找环的入口节点。接下来初始化连个指针，`ptr1`：它指向头节点， `ptr2`：指向第一阶段找到的相遇节点。然后将他们以一次移动一个节点的速度向前移动，直到他们再次相遇为止，并返回这个节点。

看下图来帮助我们理解：







![Phase 2 diagram](https://leetcode.com/articles/Figures/142/diagram.png)







2⋅distance(tortoise)2(F+a)2F+2aF=distance(hare)=F+a+b+a=F+2a+b=b2⋅distance(tortoise)=distance(hare)2(F+a)=F+a+b+a2F+2a=F+2a+bF=b

- 时间复杂度 : *O*(*n*)

  在环中 `hare` 和 `tortoise` 在经过*F*+*C*−*h* 个迭代后相遇，*F*+*C*−*h*≤*F*+*C*=*n*,所以第一个阶段时间复杂度为*O*(*n*)  ，第二阶段走了 *F*<*n*  个迭代，所以总的时间复杂度也就是*O*(*n*) 。

- 空间复杂度 : *O*(1)

代码

```java
public class Solution {
    private ListNode getIntersect(ListNode head) {
        ListNode tortoise = head;
        ListNode hare = head;
 
        // A fast pointer will either loop around a cycle and meet the slow
        // pointer or reach the `null` at the end of a non-cyclic list.
        while (hare != null && hare.next != null) {
            tortoise = tortoise.next;
            hare = hare.next.next;
            if (tortoise == hare) {
                return tortoise;
            }
        }
 
        return null;
}
 
    public ListNode detectCycle(ListNode head) {
        if (head == null) {
            return null;
        }
 
        // If there is a cycle, the fast/slow pointers will intersect at some
        // node. Otherwise, there is no cycle, so we cannot find an entrance to
        // a cycle.
        ListNode intersect = getIntersect(head);
        if (intersect == null) {
            return null;
        }
 
        // To find the entrance to the cycle, we have two pointers traverse at
        // the same speed -- one from the front of the list, and the other from
        // the point of intersection.
        ListNode ptr1 = head;
        ListNode ptr2 = intersect;
        while (ptr1 != ptr2) {
            ptr1 = ptr1.next;
            ptr2 = ptr2.next;
        }
 
        return ptr1;
    }
}
```