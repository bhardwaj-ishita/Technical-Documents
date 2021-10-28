# algorithms:

### 1) binary search algorithm

it is a divide and conquer algorithm

it is a searching technique

only efficient when the arrays are already sorted

also used to find max and min element in the array

at every iteration search space reduces in half as it eliminates half of the values 

hence efficient than linear search

##### pseudocode

```java
int start = 0;
int end = array.length-1;
int mid = (start + end)/2;

if(value == mid) return mid;
else if(value < array[mid]) {
    //RHS discarded
    start = 0;
    end = mid-1;
}
else if(value > array[mid]) {
    //LHS discarded
    start = mid + 1;
    end = length -1;
}
```

##### iterative method

```java
while(start < end) {
    mid = (start + end)/2;
    if (value == array[mid]) return mid;
    else if(value < array[mid]) {
        end = mid - 1;
    }
    else if(value > array[mid]) {
        start = mid + 1;
    }
}
return null;
```

##### recursive method

```java
public static function(int[] array, int start, int end, int value) {
    if(start >= end) return -1;
    int mid = (start + end)/2;
    if(value == array[mid]) return mid;
    else if(value > array[mid]) return function(array, mid+1, end, value);
    else return function(array, start, mid-1, value);
}
```

##### time complexity

at each iteration the search space becomes half

best case: when the first mid value == required value ==> O(1)

worst/average case: O(log n)

###### compute time complexity

let number of iterations be k

size of the array = n

at iteration 1: n/(2)^0^

at iteration 2: n/(2)^1^

at iteration 3: n/(2)^2^

at iteration k: n/(2)^k^ == 1

n = 2^k^

log (n) = k log(2)

k = log n

##### space complexity

iterative method: looping structure is used and it is an in-place algorithm, hence O(1)

recursive method: stacks are used for k iterations, hence O(log n)

##### integer overflow

instead of mid = (start + end)/2

use mid = end - (start+end)/2; or mid = start - (start + end)/2;



-----------------------------------------------------------------------------------------------------------------------------------------------------------



### 2) breadth first search algorithm

for traversing/searching in a tree or graph

explores the neighbors before moving to next level neighbors

explores the vertices in the order of their distance from left to right (or mostly depends on the question)

##### pseudocode

```java
//Tree Traversal
queue.offer(root);
while(queue.isNotEmpty()) {
    Node = queue.poll();
    sout(node.val);
    if(left!=null) queue.offer(left);
    if(right!=null) queue.offer(right);
}
```

##### tree iterative method

```java
class Node{
    Node left;
    Node right;
    int data;
    
    Node(int data) {
        this.data = data;
        left = right = null;
    }
}

class BinaryTree{
    Node root;
    
    public static List<Integer> BFS(Node root) {
        List<Integer> list = new ArrayList<>();
        if(root==null) return list;
        Queue<Node> q = new LinkedList<>();
        q.add(root);
        while(!q.isEmpty()) {
            Node curr = q.poll();
            list.add(curr.data);
            if(curr.left!=null) q.offer(curr.left);
            if(curr.right!=null) q.offer(curr.right);
        }
        return list;
    }
}
```

time complexity: O(n)

space complexity: O(n)

##### tree recursive method 

```java
public Queue<Node> q = new LinkedList<>();
public static void BFS(Node root) {
    if(q.isEmpty) return;
    if(root==null) return;
    q.add(root);
    Node curr = q.poll();
    sout(curr.data);
    if(curr.left!=null) BFS(curr.left);
    if(curr.right!=null) BFS(curr.right);
}
```

time complexity: O(n)

space complexity: O(n)

##### pseudocode

```java
int v = number of vertices;
int AdjacencyList[v].LinkedList<Integer>();//stores the vertex and it's edges
boolean[v] visited;
Queue<Integer> queue = new LinkedList<>();
int rootVal; (given)

visited[rootVal] = visited == true;
queue.add(rootVal);
while(queue.isNotEmpty) {
    value = queue.poll();
    sout(value);
    for(Iterator iter: adjacencyList[value].hasNext) {
        int n = iter.next();
        if(visited[n]==notvisited==false) {
            visited[n] = true;
            queue.add(n);
        }
    }
}
```

##### graph iterative method

```java
class Graph{
    int V;//vertices
    LinkedList<Integer> adj[];//adjacency list
    
    Graph(int v){
        V = v;
        adj = new LinkedList[v];
        //making a linked list at every index for every vertex to
        //store their neighbours
        for(int i = 0; i < v; ++i) adj[i] = new LinkedList();
    }
    
    public void BFS(int value) {
        //the visited storage, will tell which nodes are visited or not
        boolean[] visited = new boolean[v];
        //queue for BFS
        LinkedList<Integer> queue = new LinkedList<>();
        //the root node is visited hence true
        visited[value] = true;
        queue.add(value);
        
        //while we've not reached all the connected nodes the loop will go on
        while(!queue.isEmpty()){
            int v = queue.poll();
            sout(value);
            //iterator will search the neighbouring nodes of the current node(the 
            //linked list at that index)
            Iterator<Integer> iter = new adj[value].listIterator();
            while(iter.hasNext()) {
                int n = iter.next;
                //if not visitd then it is visited and enqueued
                if(!visited[n]) {
                    visited[n] = true;
                    queue.add(n);
                }
            }
        }
    } 
}
```

##### graph recursive method

```java
public boolean[] visited = new boolean[v];
public Queue<Integer> queue = new LinkedList<>();
public void BFS(int value) {
    if(queue.isEmpty) return;
    visited[value] = true;
    queue.add(value);
    int v = value = queue.poll();
    sout(value);
    Iterator<Integer> iter = new adj[value].listIterator();
    while(iter.hasNext()) {
        int n = iter.next;
        if(!visited[n]) {
            visited[n] = true;
            queue.add(n);
        }
    }
    BFS(q.peek());
} 
```

in case of disconnected graph, after all the connected nodes are visited; we apply BFS individually for all the unvisited nodes in the adjacency list

time complexity: O(V+E) == all the vertices visited and their edges 

O(E) may vary from O(1) to O(V^2^) depending on how dense the graph is



-----------------------------------------------------------------------------------------------------------------------------------------------------------



### 3) depth first search algorithm

traverse each node without repeating a node (in graph)

just like trees their are three types of dfs traversals: pre, post, in

first traversal is done in depth of each adjacent node and then backtracks to traversing another adjacent node

stack is used in iterative mode

##### in trees

```java
//pre order traversal: visit each node before it's children
public void preOrder(Node node) {
    if(node==null) return;
    sout(node.val);
    preOrder(node.left);
    preOrder(node.right);
}

//post order traversal: visit each node after it's children 
public void preOrder(Node node) {
    if(node==null) return;
    preOrder(node.left);
    preOrder(node.right);
    sout(node.val);
}

//in order traversal: visit left then root and then right
public void preOrder(Node node) {
    if(node==null) return;
    preOrder(node.left);
    sout(node.val);
    preOrder(node.right);
}
```

time complexity: O(n)

space complexity: O(n)

##### in graphs

```java
//basic pseudo code
public void DFS(int v, boolean[] visited) {
    visited[v] = true;
    sout(v);
    for(int u: adj.get(v)) {
        if(!visited[u]) DFS(u,visited);
    }
}

//all the preparaions that you need to do to do the DFS
public ArrayList<Integer> dfsOfGraph(
    int V, 
    ArrayList<ArrayList<Integer>> adj)
    {
        boolean[] visited = new boolean[V];//make visited boolean matrix
        ArrayList<Integer> list = new ArrayList<>();//to save the solution
        return DFS(0,adj, visited, list);

    }

    public ArrayList<Integer> DFS(
        int v, 
        ArrayList<ArrayList<Integer>> adj,
        boolean[] visited, 
        ArrayList<Integer> list)
    {
        visited[v] = true;
        list.add(v);
        for(int u: adj.get(v)){
            if(!visited[u]) {
                DFS(u,adj,visited,list);
            }
        }
        return list;
    }
```

time complexity: O(V+E)

space complexity: O(V) Since an extra visited array is needed of size V



-----------------------------------------------------------------------------------------------------------------------------------------------------------



### 4) sorting algorithms

##### insertion

here the comparison takes place only between the adjacent indices. We only care about the neighbour

there are two pointers: iteration and and pointer

the pointer will compare to the iteration pointer which is adjacent left to the pointer

if pointer < iteration then they’ll swap

else iteration will go to it’s next adjacent left until it reaches the  0th index.   

```java
public void insertionSort(int[] a) {
    for(int i = 1; i < a.length; i++) {
        int temp = a[i];
        for(int j = i-1; j >= 0 && a[j] > temp; j--) a[j + 1] = a[j];
        a[j + 1] = temp;
    }
}
```

Time Complexity: O(n^2^) 

Auxiliary Space: O(1)

Boundary Cases: Insertion sort takes maximum time to sort if elements are sorted in reverse order. And it takes minimum time (Order of n) when elements are already sorted.

Algorithmic Paradigm: Incremental Approach (sorting takes place from the starting)

Sorting In Place: Yes

Stable: Yes

Online: Yes

Uses: Insertion sort is used when number of elements is small. It can also be useful when input array is almost sorted, only few elements are misplaced in complete big array.



##### selection

here we maintain two sub arrays. one is sorted and the other is unsorted

we find the smallest element in the unsorted sub array and swap with the next to last element in the sorted array.

```java
public void selectionSort(int[] a) {
    for(int i = 0; i < a.length-1; i++) {
        int index = i;
        for(int j = i+1; j < a.length; j++) {
            if(a[j]<a[i]) index = j;
        }
        swap = (i, j, a);
    }
}
```

Time Complexity: O(n^2^) as there are two nested loops.
Auxiliary Space: O(1) 
The good thing about selection sort is it never makes more than O(n) swaps and can be useful when memory write is a costly operation. 



##### merge

divide and conquer algorithm

includes two stages: divide and merge

we’ll start dividing the array from the mid until all the indexes are individual arrays i.e. size of array == 1

```java
public void divide(int[] a, int start, int end) {
    if(end-start<2) return;
    int mid = (end+start)/2;
    divide(a,start,mid);
    divide(a,mid,end);
    merge(a,start,mid,end);
}

public void merge(int[] a, int start, int mid, int end) {
    //optimization 1
    if(a[mid-1] <= a[mid]) return;//if already sorted then return
    
    int i = start;
    int j = mid;
    int pointer = 0;
    int[] temp = new int[end-start];
    while(j < end && i < mid) {
        temp[pointer++] = a[i] > a[j] ? a[j++] : a[i++];
    }

    //optimization 2
    System.arrayCopy(a,i,a,start+pointer,mid-1);
    System.arrayCopy(temp, 0, a, start, pointer);
}
```

only when the index at i is greater than j then it'll needed to be put at the end

a = array from where you want to copy, 
i = the index where you want to copy, 
a= the array at where you want to copy, 
start + pointer = (index of temp) the index to where you want to copy finally,
(we'll directly copy it to input index instead of copying it to temp and then again to input index)
mid-1 = the last index till where you want to copy);
we won't copy if j > i because it is already at it's righteous position in the input index



Time Complexity: Sorting arrays on different machines. Merge Sort is a recursive algorithm and time complexity can be expressed as following recurrence relation. 
T(n) = 2T(n/2) + θ(n)

The above recurrence can be solved either using the Recurrence Tree method or the Master method. It falls in case II of Master Method and the solution of the recurrence is θ(nLogn). Time complexity of Merge Sort is  θ(nLogn) in all 3 cases (worst, average and best) as merge sort always divides the array into two halves and takes linear time to merge two halves.
Auxiliary Space: O(n)
Algorithmic Paradigm: Divide and Conquer
Sorting In Place: No in a typical implementation
Stable: Yes



##### quick

divide conquer algorithm

picks a pivot and arranges all the elements according to it

pivot can be picked in many different ways: take the first element as the pivot, or the last, or any random or the mid number

pick an index and if the element is greater than pivot then put it after pivot else if the element is smaller than pivot then put it before  the pivot

and then go on the 2 sub arrays: the segment before the pivot and the segment after the pivot and again quicksort it.

```java
public void quickSort(int[] a, int start, int end) {
    if(end-start < 2) return;
    int pivot = a[start];
    int i = start;
    int j = end;
    while(i <  j) {
        while(i < j && a[j] >= pivot) --j;
        if(i < j) a[i] = a[j];
        while(i < j && a[i] <= pivot) ++i;
        if(i < j) a[j] = a[i];
    }
    a[j] = pivot;
    quickSort(a, start,j);
    quickSort(a,j+1,end);
}
```

not stable but can be made stable

in place

worst case when the pivot picked is the smallest or largest element of the array

best case when the pivot picked is a middle most number

quicksort is better for arrays and mergesort is better

O(nlogn) Time complexity



##### counting

keys between a specific range. 

It works by counting the number of objects having distinct key values (kind of hashing)

```java
public void countingSort(int[] a) {
    int max = Arrays.stream(a).max().getAsInt();
    int min = Arrays.stream(a).min().getAsInt();
    int[] count = new int[max-min+1];
    int[] output = new int[a.length];
    for(int i = 0; i < a.length; i++) {
        count[a[i]-min]++;
    }
    int j = 0;
    for(int i = 0; i < count.length;) {
        output[j++] = a[i] + min;
        count[a[i]-min]--;
        if(count[a[i]-min]==0)i++;
    }
    
    
}
```



##### heap

-----------------------------------------------------------------------------------------------------------------------------------------------------------



### 5) kadane’s algorithm

##### Q. find the sum of contiguous subarray within a one-dimensional array of numbers that has the largest sum

A train goes on of numbers and they keep adding up as we go forward
only the next number decides if it should join the train and add up to it OR start it's own train
Basically see if the number is bigger than all the numbers added up together

```java
int osum = a[0];
int csum = a[0];
for(int i = 0; i<n; i++) {
    if(csum > 0) csum += a[i]; //agar peeche se sum positive aa rha hai toh a[i] decides 
    							//to join the csum

    else csum = a[i];//agar peeche se sum ghate main aa rha hai toh a[i] decides to start 
    				//to make their own sum
    				//jaha ham khade hote hai whi se line shuru ho jati hai
    

    if(csum > osum) osum = csum;
}
return osum;
```

we’ll keep adding until we find a better option

if the current sum is going on to be positive, just keep adding

if at any point it goes negetive and the index is more negetive we start a new subarray

and compare to the maxSubArray saved until now if it is greater then let it be else update it with the currentSubArray

**Time Complexity:** O(n)

-----------------------------------------------------------------------------------------------------------------------------------------------------------



### 6) quick-select algorithm

##### Q. find the kth smallest or largest element

uses partitioning

- partition using the last number.
- compare all the numbers in the array with the last number
- and if the number is larger leave 
- else if small or equal write the number 
- and then write all the bigger numbers to the left 

now see if the number you want is kth smallest number then see if the index (k-1) belongs in the right partition or the left

- if the number is not in right then again partition the left
- else if the number is in right then send partition the right

```java
public int quickSelect(int[] a, int start, int end, int k) {
    if(end-start < 2) return;
    int pivot = a[start];
    int i = start;
    int j = end;
    while(i <  j) {
        while(i < j && a[j] >= pivot) --j;
        if(i < j) a[i] = a[j];
        while(i < j && a[i] <= pivot) ++i;
        if(i < j) a[j] = a[i];
    }
    a[j] = pivot;
    
    if(j = k) return pivot;
    else if(k < j) return quickSelect(a, start,j, k);
    else return quickSelect(a,j+1,end, k); 
}
```

1. Like quicksort, it is fast in practice, but has poor worst-case performance. 
2. The partition process is same as QuickSort, only recursive code differs.
3. There exists an algorithm that finds [k-th smallest element in O(n) in worst cas](https://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array-set-3-worst-case-linear-time/)e, but QuickSelect performs better on average.





-----------------------------------------------------------------------------------------------------------------------------------------------------------



### 7) union-find

disjoint set ds is a data structure which keeps track of non-overlapping subsets

union find is one of the algorithm which can be applied to this data structure

union find uses two very powerful operations on this data structure: find and union

##### find:

determines which subset a particular element is in. can be used to determine if two elements are in the same subset. by same subset we mean they have same parent

##### union: 

join two subsets into a single subset

one of the very common use of union find is to check whether an undirected graph contains cycle or not



this data structure is represented by a tree which holds a reference to its parent of each node and representative of each “set tree” is the root itself

or you can use an array to write the parent of the node. just like an adjacency list

Find : follows the parents until it reaches the root

Find returns the representative of the node Find(4) = 3 (where 3 is the parent of the root)

Union: combines two trees into one by attaching one tree’s root into root of other

```java
class UF{
    public int count = 0;
    public int[] id = null;

    public UF(int m, int n, char[][] grid) {
        for(int i = 0; i < n; i++) {
            for(int j = 0; j < m; j++) {
                if(grid[i][j] == '1') count++;
            }
        }
        id = new int[m*n];

        //here we are assiging evey node as it's own parent or you can assign -1 as it's parent
        for(int i = 0; i < m * n; i++) id[i] = i;
    }

    public int find(int index) {
        int parent = id[index];
        while(index != parent) {//jab tak we don't find an index which is it's own parent
            index = parent;//now we'll make the parent the node
            parent = id[parent];//and make the id[parent] as the new parent
        }
        return index;
    }

    public void union(int p, int q) {
        int parentP = find(p);
        int parentQ = find(q);
        if(parentP == parentQ) return;
        id[parentP] = parentQ;
    }

    public boolean isConnected(int p, int q) {
        int parentP = find(p);
        int parentQ = find(q);
        if(parentP != parentP) return false;
        else return true;
    }
}

```

Note that the implementation of *union()* and *find()* is naive and takes O(n) time in the worst case.



-----------------------------------------------------------------------------------------------------------------------------------------------------------



### 8) kruskal

##### what is a minimum spanning algorithm?

connected undirected graph

it is a tree which is connects all the vertices with minimal total weighting for its edges

It has n-1 edges and n vertices and the sum of the weights of edges is minimum as possible.

##### algorithm

the algo is simple we'll start picking the edges and it's respective vertices from the smallest weighing edge and if the edge creates a circular graph then we'll discard it until we find all the nodes connected 

then we'll discard all the non visited edges too.

 

```
//sort all edges in graph in increasing order of their weight
while(v-1 times) {
    //start from the min edge value and check if it is connected to 	an 	already visited node
        if (yes) then go to the next smallest weighing edge(i.e find 			if it forms a cycle with the graph if not then add to the 				MST)
         else this edge is a part of the MST
}
```



if the graph is not connected then, Kruskal finds a Minimum Spanning Forest i.e MST for each connected component of the graph

```java
Collections.sort(list, (weight,edge) -> this.weight - list.weigjt);
```



-----------------------------------------------------------------------------------------------------------------------------------------------------------



### 9) floyd warshall





-----------------------------------------------------------------------------------------------------------------------------------------------------------



### 10) dijkstra



-----------------------------------------------------------------------------------------------------------------------------------------------------------



### 11) bellman



-----------------------------------------------------------------------------------------------------------------------------------------------------------



### 12) lee



-----------------------------------------------------------------------------------------------------------------------------------------------------------



### 13) floodeill



-----------------------------------------------------------------------------------------------------------------------------------------------------------



### 14) floyd cycle detection



-----------------------------------------------------------------------------------------------------------------------------------------------------------



### 15) topological sort

only for the DAG (Directed Acyclic Graphs)

linear ordering of vertices such that for every directed edge u,v; u comes before v in ordering

the first vertex (starting index) is always a vertex with no **incoming** edges i.e in-degree as 0

<img src="C:\Users\ishit\Downloads\Screenshot 2021-08-08 132105.png" style="zoom:50%;" />

their can be many topological sort of one DAG

542310 or 452310

5 and 4 both have no  incoming edges 

##### topological sort V/S depth first traversal

In [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/), we print a vertex and then recursively call DFS for its adjacent vertices. 

In topological sorting, we need to print a vertex before its adjacent vertices. 

For example, in the given graph, the vertex ‘5’ should be printed before vertex ‘0’, but unlike [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/), the vertex ‘4’ should also be printed before vertex ‘0’. So Topological sorting is different from DFS. For example, a DFS of the shown graph is “5 2 3 1 0 4”, but it is not a topological sorting.

```java
public static int[] topoSort(int V, ArrayList<ArrayList<Integer>> adj)
    {
        // add your code here
        boolean[] visited = new boolean[V];

        for(boolean i : visited) i = false;

        Stack<Integer> stack = new Stack<Integer>();

        for(int i = 0 ; i < V; i++) {
            if(!visited[i]) DFS(0,adj,stack,visited);
        }

        int[] ans =new int[stack.size()];
        int i = 0;

        while(!stack.isEmpty()) ans[i++] = stack.pop();
        return ans;
    }

    public static void DFS(int v, ArrayList<ArrayList<Integer>> adj, Stack<Integer> stack, boolean[] visited) {
        visited[v] = true;
        for(int u : adj.get(v)) {
            if(!visited[u]) DFS(u,adj,stack,visited);
        }
        stack.push(v);
    }
```

- **Time Complexity:** O(V+E). 
  The above algorithm is simply DFS with an extra stack. So time complexity is the same as DFS which is.
- **Auxiliary space:** O(V). 
  The extra space is needed for the stack.



##### detect cycle using topological sort

one of the ways to detect cycle in an directed graph is by using topological sort
We can assume from the starting that the graph is DAG
and if we are not able to form the TS of the graph then it has a cycle

Our main focus is to keep checking if the parent of a child is the child's child too somewher
if yes then it's a cycle

And unlike undirected graph where we only need to check the root parent
here we keep the nodes(parents) in a hierarchy as we always have to keep looking for the immediate parent

```java
public boolean canFinish(int n, int[][] pre) {
        boolean[] visited = new boolean[n];
        for(boolean i : visited) i = false;

        ArrayList<ArrayList<Integer>> adj = new ArrayList<>();
        for(int i = 0; i < n; i++) adj.add(new ArrayList<Integer>());
        for(int i = 0; i < pre.length; i++) adj.get(pre[i][1]).add(pre[i][0]);

        Stack<Integer> stack = new Stack<>();

        for(int i = 0; i < n; i++) {
            if(!visited[i]) DFS(i, adj,stack, visited);
        }
        
        int ind = 0;
        HashMap<Integer,Integer> map = new HashMap<>();
        while(!stack.isEmpty()) {
            map.put(stack.pop(),ind);
            ind++;
        }

        for(int i = 0; i < n; i++) {
            for(int u: adj.get(i)) {
                if(map.get(i) >= map.get(u)) return false;
            }
        }
        return true;

    }

    public void DFS(int v ,ArrayList<ArrayList<Integer>> adj, Stack<Integer> stack, boolean[] visited) {
        visited[v] = true;
        for(int u : adj.get(v)) {
            if(!visited[u]) DFS(u,adj,stack,visited);
        }
        stack.push(v);

    }
```





-----------------------------------------------------------------------------------------------------------------------------------------------------------



### 16) kmp



-----------------------------------------------------------------------------------------------------------------------------------------------------------



### 17) kahn’s topological sort

we have already done TS using a DFS based solution. 

we know that TS is only possible in a DAG Graph

and we also know that a DAG graph always have one vertex with in-degree 0 and one with out-degree 0

-----------------------------------------------------------------------------------------------------------------------------------------------------------



### 18) huffman coding compression



-----------------------------------------------------------------------------------------------------------------------------------------------------------



### 19) boyer-moore majority vote 



-----------------------------------------------------------------------------------------------------------------------------------------------------------



### 20) euclid



-----------------------------------------------------------------------------------------------------------------------------------------------------------

