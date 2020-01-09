**Binary Search tree**

```java
package BST;

public class BSTNode {
	public BSTNode leftChild;
	public BSTNode rightChild;
	public BSTNode parent;
	
	int data;
	int count;
	boolean find = false;
	
	public BSTNode() {
		rightChild = null;
		leftChild = null;
		parent = null;
		data = 0;
	}
	
	public BSTNode(int data) {
		parent = null;
		rightChild = null;
		leftChild = null;
		this.data = data;
	}
	
	public BSTNode searchBST(BSTNode par, int data) {
		BSTNode curr = par;
		
		count++;
		
		if(find == false && curr == null)
			return curr;
		else if(curr.data > data)
			curr = searchBST(curr.leftChild, data);
		else if(curr.data < data)
			curr = searchBST(curr.rightChild, data);
		else
			find = true;
		
		return curr;
	}
	
	public BSTNode addBST(BSTNode par, int data) {
		BSTNode curr = par;
		
		if(curr == null) {
			BSTNode newNode = new BSTNode(data);
			curr = newNode;
			return curr;
		}
		else if(curr.data > data) {
			curr.leftChild = addBST(curr.leftChild, data);
			curr.leftChild.parent = curr;
			return curr;
		}
		else if(curr.data < data) {
			curr.rightChild = addBST(curr.rightChild, data);
			curr.rightChild.parent = curr;
			return curr;
		}
		else {
			return curr;
		}

	}
	
	public BSTNode deleteBST(BSTNode parent, BSTNode curr, int data){
		BSTNode delNode = curr;
		
		if(delNode == null) {
			System.out.println("데이터를 발견하지 못했습니다.");
			return null;
		}
		//탐색 부분
		else if(delNode.data > data) {
			curr.leftChild = deleteBST(curr, curr.leftChild, data);
			return curr;
		}
		
		else if(delNode.data > data) {
			curr.rightChild = deleteBST(curr, curr.rightChild, data);
			return curr;
		}
		
		else {
			if(curr.leftChild != null || curr.rightChild != null) {
				BSTNode temp;
				if (curr.leftChild != null) {
					temp = BST_FindMax(curr.leftChild);
					curr.data = temp.data;
					curr.leftChild = deleteBST(curr, curr.leftChild, curr.data);
				}
				
				else {
					temp = BST_FindMin(curr.rightChild);
					curr.data = temp.data;
					curr.rightChild = deleteBST(curr, curr.rightChild, curr.data);
				}
				
			}
			
			//leaf 노드
			else {
				if(parent.leftChild.equals(curr))
					parent.leftChild = null;
				else if(parent.rightChild.equals(curr))
					parent.rightChild = null;
				return null;
			}
		}

		
		return curr;
	}

	public BSTNode BST_FindMax(BSTNode curr) {
		if(curr.rightChild != null) {
			return BST_FindMax(curr.rightChild);
		}
		return curr;
	}
	
	public BSTNode BST_FindMin(BSTNode curr) {
		
		if(curr.leftChild != null) {
			return BST_FindMax(curr.leftChild);
		}
		return curr;
	}
}
```
