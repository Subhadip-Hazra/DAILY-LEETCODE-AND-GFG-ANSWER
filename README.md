# 08-May GFG answer 

# [Root to Leaf Paths](https://www.geeksforgeeks.org/problems/root-to-leaf-paths/1)

### Given a Binary Tree of nodes, you need to find all the possible paths from the root node to all the leaf nodes of the binary tree.

**Example 1:**

**Input:**
```
       1
    /     \
   2       3
```
**Output:**
```
1 2 
1 3 
```
**Explanation:** 
All possible paths:
1->2
1->3

**Example 2:**

**Input:**
```
         10
       /    \
      20    30
     /  \
    40   60
```
**Output:** 
```
10 20 40 
10 20 60 
10 30 
```

**Your Task:**
Your task is to complete the function `Paths()` which takes the root node as an argument and returns all the possible paths. (All the paths are printed in new lines by the driver's code.)

**Expected Time Complexity:** O(n)
**Expected Auxiliary Space:** O(height of the tree)

**Constraints:**
1 ≤ n ≤ 10^4

``` JAVA
  class Solution {
    public static ArrayList<ArrayList<Integer>> Paths(Node root) {
        // code here
        ArrayList<ArrayList<Integer>> res = new ArrayList<>();
        if( root == null) return res;
        ArrayList<Integer> path = new ArrayList<>();
        findPath(root,path,res);
        return res;
    }
    public static void findPath( Node root, ArrayList<Integer> path , ArrayList<ArrayList<Integer>> res){
        path.add( root.data );
        if( root.left == null && root.right == null){
            res.add(new ArrayList<>(path));
        }
        else{
            if( root.left != null){
                findPath(root.left,path,res);
            }
            if(root.right != null){
                findPath(root.right,path,res);
            }
        }
        path.remove(path.size() - 1);
    }
}
```
## TIME COMPLEXITY:
we have to traverse all nodes so the time complexity is O(n)

## SPACE COMPLEXITY:
the space complexity is also O(n), same we have to traverse all nodes.

## DISCUSSION
So, what question is do we have to store all depth-wise node values in a list for every every different depth we have to store the values in a different list 
and in the final result, we have to store all the lists in one list and that will be the final result.

## APPROACH
There are many approaches but we discuss about the Recursive approach
#### Let's dry-run our code 
We take this example
```
         10
       /    \
      20    30
     /  \
    40   60
```
This is our final list     

```
    [[                 ]]  This is our final list currently it is empty
```
```
    [                   ]  This is our path list that stores every depth node value.
```

```
                                                               10______________  Step 1: root != null so, we go to the next step which calls the find path function 
                                                             /    \
step2:we entered the find path function __________________  20    30
                                                           /  \
                                                          40   60


step2: path [ 10,            ]       res [         ]   root = 10
        the root value is added to the root
        and, the first condition is false because it has leaves
        in secondition at first we check for the root left hand. OOh, the condition is satisfied it calls the find path function
        public static void find path( Node root, ArrayList<Integer> path , ArrayList<ArrayList<Integer>> res){
        path.add( root.data );
        if( root.left == null && root.right == null){
            res.add(new ArrayList<>(path));
        }
        else{
            if( root.left != null){
                find path(root.left,path,res);
            }
            if(root.right != null){
                findPath(root.right,path,res);
            }
        }
        path.remove(path.size() - 1);
    }

step 2.1:  path [ 10 , 20      ]  res [          ]     root = 20                     10
      20 add to the list because the current root value = 20                         /
      first IF condition is false because it leaves                              20
      again is called find path   ---------> step 2.2                            /
                                                                             40

step 2.2:  path [ 10 , 20 , 40 ]  res [          ]     root = 40               
      40 add to the list because current root value = 40                  20
      first IF condition is true                                         /
      now, it will add the full list to the final list,               40
      so it satisfies the first condition and will go to the 

      path.remove(path.size() - 1);  ( basically, It will help to backtrack )
      so, this line of code will remove the last element of the path list
      it completes a full rotation but, you can see there are two if conditions so what rotation is complete for STEP 2.1 where we call the function.
      if( root.left != null){
                find path(root.left,path,res);   
            }
      if(root.right != null){
          findPath(root.right,path,res);
      }
      now we check for the root's right hand ok, we have a node that has a value of 60      
      so, we go to the step 2.1.1


STEP 2.1.1 : path [ 10, 20 , 60 ]  res= [[ 10, 20 , 40 ]]   root =60                            60
         so, our root has no leaves so we add the path to our final list                       /  \
         and one element will be deleted from our list                                      null    null                                   
          from our list  and our 2.1.1 rotation is complete                                                                             
          ok, step 2.1 root right hand checked
          and another element will be removed from the list
          finally, the step 2.1 rotation is complete.

                     
                        * 10
                        /    \
                   *  20      30     [ * means visited ] 
                     /  \
                  * 40   60 *

          but remember we check for root left hand in STEP 2
          where we have to check for the root right hand.                                                                            

STEP 3 : path [ 10,30  ]   res = [[ 10 , 20 , 40 ]]    root = 30
                            [ [ 10 , 20 , 60 ] ]
      now, the 30 is added to our path list but the root node has no leaves so here all traverse is ended and now our root is null and no checking
      and finally the path list will be added to the res list
      so, the final result is
        [[ 10,20,40 ]]
        [[ 10,20,60 ]]
        [[ 10,30 ]]

```

`The recursive approach dry run is very complex but I try my best `
If you want more this type of content like this then `follow me` on [Github](https://github.com/subhadip-hazra) and [Linkedin](https://www.linkedin.com/in/subhadiphazra/)



























