# Linked List

## Notes

* Dummy nodes are helpful when maniuplating nodes and there is fear that the head might be manuipilated . Create dummy -> point it to head -> get previous -> set previous to dummy and do your calculation ... so since the two nodes (dummy and previous node are the same, the calculations we do at previous node will affect dummy )

```
d = Node("dummy") # 1
    d.next = head
    p = d
    // both p and d have next set to m
    p.next = m
    // p is now moved and points to null but d is still pointing to m
    p = p.next
    
```
