# Smallest-String-Starting-From-Leaf
You are given the root of a binary tree where each node has a value in the range [0, 25] representing the letters 'a' to 'z'.  Return the lexicographically smallest string that starts at a leaf of this tree and ends at the root.


class Solution:
    def smallestFromLeaf(self, root: Optional[TreeNode]) -> str:
        def dfs(node, path, smallest):
            if not node:
                return
            
            path.append(chr(node.val + ord('a')))
            
            if not node.left and not node.right:
                current_string = ''.join(path[::-1]) 
                smallest[0] = min(smallest[0], current_string)
            
            dfs(node.left, path, smallest)
            dfs(node.right, path, smallest)
            
            path.pop()
        
        smallest = [chr(ord('z') + 1)]  
        
        dfs(root, [], smallest)
        
        return smallest[0]
