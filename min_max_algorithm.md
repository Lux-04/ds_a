# Min Max Algorithm

## Recursion

The Min Max algorithm is used in problems that require two players trying to maximize their scores. The general gist of the algorithm is that 
one player acts as a maximizer to the score and one player acts as a minimize. The winner can be determined by whether the final score is positive
or negative.

The goal of the Min Max algorithm is to determine the result of the game if both players are playing optimally.

In order to find the optimal moves for both players, we must exhaustively look through the search tree for all possible moves a player can make.
Once the last move of a player is made(the base case) we backtrack and evaluate which move is optimal for each player. The final score will till us
the winner of the game.

Consider the problem: https://leetcode.com/problems/predict-the-winner/

An example is below:


The total running time of this algorithm is O(2<sup>n</sup>) As we must exhaustively search through a binary tree.

An example implementation of the problem above is below: 

```ruby
class Solution {
    public boolean PredictTheWinner(int[] nums) {
        #Final score
        int score = recursion(nums,0,nums.length-1,true);
        #Player one wins if score is above or equal to 0.
        if (score >= 0) {
            return true;
        }
        #Else player two wins.
        return false;
    }
    
    
    #We keep track of the left index and right index that a player can pick from. We also keep track of which player's turn it is.
    #true denotes it's player 1's turn and we should add to the score, false denotes it's player 2's turn and we should subtract from the score.
  
    #In each recursive call we compute the optimal pick from choosing from the left and the right for both players. If the left index equals the right
    #index this indicates that there is only one pick a player can make and thus is our base case.
    
    private int recursion(int[] nums, int l, int r, boolean player) {
        #Base case when when no more elements to pick
        if (l == r && player) {
            return nums[l];
        }
       
        #Base case for player 2, we subtract instead to minimize the score.
        else if (l == r && !player) {
            return -nums[l];
        }
        int a,b;
        
        #For both players we compute both scenarios, left and right by recursively solving till the end of the game and backtracking,
        #picking the optimal solution at each step.
        
        if (player) {
            a = nums[l] + recursion(nums,l+1,r,false);
            b = nums[r] + recursion(nums,l,r-1,false);
        }
        
        #For player 2 we subtract the current pick as they are the minimizer.
        else {
            a = -nums[l] + recursion(nums,l+1,r,true);
            b = -nums[r] + recursion(nums,l,r-1,true);
        }
       
       #For player 1 we return the maximum of both picks.
       if (player) {
           return Math.max(a,b);
       }
       #For player 2 we return the minimum of both picks.
        return Math.min(a,b);
    }
}
```

## Simplification

## Top-Down DP

