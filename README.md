# Coding-bot

72. Edit Distance
Solved
Medium
Topics
Companies
Given two strings word1 and word2, return the minimum number of operations required to convert word1 to word2.

You have the following three operations permitted on a word:

Insert a character
Delete a character
Replace a character

class Solution {
public:
    int solve(string& str1,string& str2,int i,int j,vector<vector<int>>& dp){
        if(i == str1.length()) return str2.length()-j;
        if(j == str2.length()) return str1.length()-i;
        
        if(dp[i][j]==-1){
            
            if(str1[i]==str2[j]){
                dp[i][j]=solve(str1,str2,i+1,j+1,dp);
            }else{
                //deletion
                int operation1 =solve(str1,str2,i+1,j,dp);

                //insertion
                int operation2 =solve(str1,str2,i,j+1,dp);

                //replace
                int operation3 =solve(str1,str2,i+1,j+1,dp);
                dp[i][j] =min({operation1,operation2,operation3})+1;
            }        
        }
        return dp[i][j];
    }
    int minDistance(string word1, string word2) {
        vector<vector<int>> dp(word1.length(),vector<int>(word2.length(),-1));
        return solve(word1,word2,0,0,dp);   
    }
};

