# LRU缓存

![截屏2022-04-01 22.48.02](https://tva1.sinaimg.cn/large/e6c9d24egy1h0ulv8rzd7j20cw0le762.jpg)



```java
package com.Seejen.java;

import java.util.HashMap;
import java.util.Map;
//最简单的数据结构就是双向链表 LinkedHashMap，面试的时候最好手写定义一个双向链表
public class Main {
    public static void main(String[] args) {
        LRUCache obj = new LRUCache(10);
        obj.put(1,1);
        System.out.println(obj.get(1));
    }
}

class LRUCache{
    private Map<Integer,DLinkedNode> cache = new HashMap<>();
    private int size;
    private int capacity;
    private DLinkedNode head,tail;

    public LRUCache(int capacity){
        this.size = 0;
        this.capacity = capacity;
        head = new DLinkedNode();
        tail = new DLinkedNode();
        head.next = tail;
        tail.prev = head;
    }

    public int get(int key){
        DLinkedNode node = cache.get(key);
        if(node == null){
            return -1;
        }
        moveToHead(node);
        return node.val;
    }

    public void put(int key,int val){
        DLinkedNode node = cache.get(key);
        if(node == null){
            DLinkedNode newNode = new DLinkedNode(key,val);
            cache.put(key,newNode);
            addToHead(newNode);
            size++;
            if(size > capacity){
                DLinkedNode tail = removeTail();
                cache.remove(tail.key);
                size--;
            }
        }
        else{
            node.val = val;
            moveToHead(node);
        }
    }

    private void addToHead(DLinkedNode node){
        node.prev = head;
        node.next = head.next;
        head.next.prev = node;
        head.next = node;
    }

    private void removeNode(DLinkedNode node){
        node.prev.next = node.next;
        node.next.prev = node.prev;
    }

    private void moveToHead(DLinkedNode node) {
        removeNode(node);
        addToHead(node);
    }
    private DLinkedNode removeTail(){
        DLinkedNode res = tail.prev;
        removeNode(res);
        return res;
    }
}

class DLinkedNode{
    int key;
    int val;
    DLinkedNode prev;
    DLinkedNode next;
    public DLinkedNode(){}
    public DLinkedNode(int key,int val){
        this.key = key;
        this.val = val;
    }
}
```

