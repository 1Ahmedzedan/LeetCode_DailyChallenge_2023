# LeetCode Daily Challenge Problems for April

<br><br>

## Workflow Checking

<div align="center">
<img src="https://github.com/7oSkaaa/LeetCode_DailyChallenge_2023/actions/workflows/Author_Line.yml/badge.svg" alt="Checkers" width="150">
<a href="https://github.com/7oSkaaa/LeetCode_DailyChallenge_2023/actions/workflows/Author_Line.yml" taget="_blank"/>
</img>
&nbsp;
<img src="https://github.com/7oSkaaa/LeetCode_DailyChallenge_2023/actions/workflows/File_Names.yml/badge.svg" alt="Checkers" width="150">
<a href="https://github.com/7oSkaaa/LeetCode_DailyChallenge_2023/actions/workflows/File_Names.yml" taget="_blank"/>
</img>
&nbsp;
<img src="https://github.com/7oSkaaa/LeetCode_DailyChallenge_2023/actions/workflows/Daily_Problem.yml/badge.svg" alt="Checkers" width="150">
<a href="https://github.com/7oSkaaa/LeetCode_DailyChallenge_2023/actions/workflows/Daily_Problem.yml" taget="_blank"/>
</img>
</div>

<br><br>

## Problems:

1. **[Binary Search](#01--binary-search)**

1. **[Successful Pairs of Spells and Potions](#02--successful-pairs-of-spells-and-potions)**
1. **[Boats to Save People](#03--boats-to-save-people)**
1. **[Optimal Partition of String](#04--optimal-partition-of-string)**
1. **[Minimize Maximum of Array](#05--minimize-maximum-of-array)**
1. **[Number of Closed Islands](#06--number-of-closed-islands)**
1. **[Number of Enclaves](#07--number-of-enclaves)**
1. **[Clone Graph](#08--clone-graph)**

<hr>
<br><br>

## 01)  [Binary Search](https://leetcode.com/problems/binary-search/)

### Difficulty

![](https://img.shields.io/badge/Easy-green?style=for-the-badge)

### Related Topic

`Array` `Binary Search`

### Code


```cpp
class Solution {
public:
    int search(vector < int >& nums, int target) {
        // the start and end of the interval that we will search in it
        int l = 0, r = nums.size() - 1;

        // Start a while loop with condition "l <= r".
        while(l <= r){
            // Declare an integer variable "m" and initialize it to the midpoint between "l" and "r".
            int m = l + (r - l) / 2;
            
            // If the value at index "m" in the "nums" vector is equal to the target integer, return "m".
            if(nums[m] == target) return m;
            
            // If the value at index "m" in the "nums" vector is less than the target integer, update "l" to "m + 1". Otherwise, update "r" to "m - 1".
            (nums[m] < target ? l = m + 1 : r = m - 1);
        }

        // If the target integer was not found in the "nums" vector, return -1.
        return -1;
    }
};
```
    

<hr>
<br><br>

## 02)  [Successful Pairs of Spells and Potions](https://leetcode.com/problems/successful-pairs-of-spells-and-potions/)

### Difficulty

![](https://img.shields.io/badge/Medium-orange?style=for-the-badge)

### Related Topic

`Array` `Two Pointers` `Binary Search` `Sorting`

### Code


```cpp
class Solution {
public:

    // Inline function to calculate the ceil value
    inline long long ceil(long long a, long long b){
        return (a + b - 1) / b;
    }

    // Function to calculate successful pairs
    vector < int > successfulPairs(vector < int >& spells, vector < int >& potions, long long success) {
        // Get the sizes of vectors
        int n = spells.size(), m = potions.size();
        
        // Sort potions vector
        sort(potions.begin(), potions.end());
        
        // Vector to store successful pairs
        vector < int > successful_pairs;
        
        for(auto& x : spells){
            // Calculate target value for a spell that will make it greater than success
            long long target = ceil(success, x);
            
            // Get the index of first potion having value greater or equal to target
            int idx = lower_bound(potions.begin(), potions.end(), target) - potions.begin();
            
            // Calculate number of successful pairs
            successful_pairs.push_back(m - idx);
        }

        // Return the vector containing number of successful pairs for each spell
        return successful_pairs;
    }
};
```
    
<hr>
<br><br>

## 03)  [Boats to Save People](https://leetcode.com/problems/boats-to-save-people/)

### Difficulty

![](https://img.shields.io/badge/Medium-orange?style=for-the-badge)

### Related Topic

`Array` `Two Pointers` `Greedy` `Sorting`

### Code


```cpp
class Solution {
public:
    // Function to calculate the number of rescue boats required
    int numRescueBoats(vector<int>& people, int limit) {
        // Sort the array in ascending order
        sort(people.begin(), people.end());
        
        // Initialize variables for left index, right index and number of boats
        int l = 0, r = people.size() - 1, boats = 0;
        
        // Iterate through the array using two pointers, one from the left and one from the right
        while(l <= r){
            // If the sum of the weights of the people at the two pointers is less than or equal to the limit, increment the left pointer
            if(people[l] + people[r] <= limit) l++;
            
            // Decrement the right pointer and increment the number of boats
            r--, boats++;
        }
        
        // Return the total number of boats required
        return boats;
    }

};
```
    
<hr>
<br><br>

## 04)  [Optimal Partition of String](https://leetcode.com/problems/optimal-partition-of-string/)

### Difficulty

![](https://img.shields.io/badge/Medium-orange?style=for-the-badge)

### Related Topic

`Hash Table` `String` `Greedy`

### Code


```cpp
class Solution {
public:
    int partitionString(string& s) {
        int partitions = 1, mask = 0;
        
        // Iterate over each character in the string
        for(auto& c : s){
            // Create a mask for the current character
            int curr_mask = (1 << (c - 'a'));
            
            // If the current mask is already present in the mask variable
            // increment the number of partitions and reset the mask variable
            if(mask & curr_mask)
                partitions++, mask = 0;
            
            // XOR the current mask with the mask variable
            mask ^= curr_mask;
        }
        
        // Return the number of partitions
        return partitions;
    }
};
```
    
<hr>
<br><br>

## 05)  [Minimize Maximum of Array](https://leetcode.com/problems/minimize-maximum-of-array/)

### Difficulty

![](https://img.shields.io/badge/Medium-orange?style=for-the-badge)

### Related Topic

`Array` `Binary Search` `Dynamic Programming` `Greedy` `Prefix Sum`

### Code


```cpp
class Solution {
public:

    // make shortcut for long long
    #define ll long long

    int minimizeArrayValue(vector < int >& nums) {
        // Lambda function that takes an integer as input and returns a boolean value indicating whether the given integer is good or not.
        auto is_good = [&](ll m){
            // If the first element in the vector is greater than the given integer, it cannot be good.
            if(nums[0] > m) return false;
            ll last = nums[0];
            
            // Loop through the vector starting from the second element.
            for(int i = 1; i < nums.size(); i++){
                // Calculate the value to be removed from the previous element to make it less than or equal to the given integer.
                ll to_remove = m - last;
                
                // Calculate the new value for the current element after removing the calculated value from the previous element.
                last = nums[i] - abs(to_remove);
                
                // If the new value is greater than the given integer, it cannot be good.
                if(last > m) 
                    return false;
            }
            
            // All elements in the vector are less than or equal to the given integer, hence it is good.
            return true;
        };
        
        // Initialize the lower and upper bounds of the binary search.
        int l = 0, r = 1e9, ans = -1;
        
        // Binary search for the minimum good integer.
        while(l <= r){
            // Calculate the middle point.
            int m = l + (r - l) / 2;
            
            // If the middle point is good, update the upper bound and the answer.
            (is_good(m) ? r = m - 1, ans = m : l = m + 1);
        }

        // Return the minimum good integer.
        return ans;
    }

};
```
    
<hr>
<br><br>

## 06)  [Number of Closed Islands](https://leetcode.com/problems/number-of-closed-islands/)

### Difficulty

![](https://img.shields.io/badge/Medium-orange?style=for-the-badge)

### Related Topic

`Array` `Depth-First Search` `Breadth-First Search` `Union Find` `Matrix`

### Code


```cpp
class Solution {
public:

    // Declare variables for the size of the grid
    int n, m;

    // make the given grid global
    vector < vector < int > > grid;

    // Check if a given cell is inside the grid.
    bool is_valid(int r, int c) {
        return r >= 0 && r < n && c >= 0 && c < m;
    }

    // DFS to traverse the grid and check if a cell is part of an island.
    bool dfs(int r, int c) {
        // If the cell is not inside the grid, return false.
        if (!is_valid(r, c)) return false;
        
        // If the cell is already part of an island, return true.
        if (grid[r][c]) return true;
        
        // Mark the cell as visited by changing its value to 2.
        grid[r][c] = 2;
        
        // Traverse all the neighbors of the cell recursively and check if they are part of an island.
        bool valid = true;
        valid &= dfs(r - 1, c);
        valid &= dfs(r + 1, c);
        valid &= dfs(r, c - 1);
        valid &= dfs(r, c + 1);
        
        // Return true if all the neighbors are part of an island, false otherwise.
        return valid;
    }

    // Function to count the number of closed islands in the grid.
    int closedIsland(vector<vector<int>>& mat) {
        // Assign the input grid to the class grid variable, and get its size.
        this -> grid = mat;
        n = grid.size(), m = grid[0].size();
        
        // Initialize the answer variable to zero, and traverse the entire grid to count the number of closed islands.
        int ans = 0;
        for (int i = 0; i < n; i++)
            for (int j = 0; j < m; j++)
                if (!grid[i][j])
                    ans += dfs(i, j);
        
        // Return the number of closed islands.
        return ans;
    }

};
```
    
<hr>
<br><br>

## 07)  [Number of Enclaves](https://leetcode.com/problems/number-of-enclaves/)

### Difficulty

![](https://img.shields.io/badge/Medium-orange?style=for-the-badge)

### Related Topic

`Array` `Depth-First Search` `Breadth-First Search` `Union Find` `Matrix`

### Code


```cpp
class Solution {
public:
    
    // Initializing two 2D vectors to store the grid values
    vector < vector < int > > grid;

    // Variables for the dimensions of the grid
    int n, m;

    // Function to check if a cell is valid
    bool is_valid(int r, int c){
        return r >= 0 && c >= 0 && r < n && c < m && grid[r][c];
    }

    // Depth first search function
    int dfs(int r, int c){
        // If the cell is not valid return 0
        if(!is_valid(r, c)) return 0;

        // Set the cell as visited
        grid[r][c] = 0;
        
        // Return 1 plus the results of the DFS of the adjacent cells
        return 1 + dfs(r + 1, c) + dfs(r, c + 1) + dfs(r - 1, c) + dfs(r, c - 1);
    }

    int numEnclaves(vector<vector<int>>& grid) {
        // Set the grid dimensions
        this -> grid = grid;
        n = grid.size(), m = grid[0].size();
                
        // Perform DFS on all cells on the border
        for(int i = 0; i < n; i++) dfs(i, 0); // left border
        for(int i = 0; i < n; i++) dfs(i, m - 1); // right border
        for(int i = 0; i < m; i++) dfs(0, i); // upper border
        for(int i = 0; i < m; i++) dfs(n - 1, i); // lower border
        
        // Count the number of enclaves by performing DFS on each valid cell
        int cnt = 0;
        for(int i = 0; i < n; i++)
            for(int j = 0; j < m; j++)
                if(is_valid(i, j))
                    cnt += dfs(i, j);
        
        // Return the count of enclaves
        return cnt;
    }

};
```
    
<hr>
<br><br>

## 08)  [Clone Graph](https://leetcode.com/problems/clone-graph/)

### Difficulty

![](https://img.shields.io/badge/Medium-orange?style=for-the-badge)

### Related Topic

`Hash Table` `Depth-First Search` `Breadth-First Search` `Graph`

### Code


```cpp
class Solution {
public:
    
    // Define an unordered map to store the nodes and their copies
    unordered_map < int, Node* > mp;

    // Define a function to clone the given graph
    Node* cloneGraph(Node* node) {
        // If node is NULL, return the node
        if (node == NULL) return node;

        // If the node already exists in the map, return its copy
        if (mp.count(node -> val)) return mp[node -> val];

        // Create a vector to store the neighbors of the current node and add the current node to the map
        mp[node -> val] = new Node(node -> val, {});

        // Recursively clone the neighbors of the current node and add them to the copy's neighbors vector
        for (auto& newNode : node -> neighbors) {
            Node* newNeighbors = cloneGraph(newNode);
            mp[node -> val] -> neighbors.push_back(newNeighbors);
        }

        // Return the copy of the given node
        return mp[node -> val];
    }
};
```
    