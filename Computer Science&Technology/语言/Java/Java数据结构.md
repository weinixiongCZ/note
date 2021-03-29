#CS/Java #CS/算法 

# 参考
- [[数据结构与算法分析 java语言描述（原书第3版）.pdf]]
- [[Java算法]]
- [[Java]]
- [[算法]]


# Queue

```java
class CircleArray {
	private final int maxSize; // 表示数组的最大容量
	//front 变量的含义做一个调整： front 就指向队列的第一个元素, 也就是说 arr[front] 就是队列的第一个元素 
	//front 的初始值 = 0
	private int front; 
	//rear 变量的含义做一个调整：rear 指向队列的最后一个元素的后一个位置. 因为希望空出一个空间做为约定.
	//rear 的初始值 = 0
	private int rear; // 队列尾
	private final int[] arr; // 该数据用于存放数据, 模拟队列
	
	public CircleArray(int arrMaxSize) {
		maxSize = arrMaxSize;
		arr = new int[maxSize];
	}
	
	// 判断队列是否满
	public boolean isFull() {
		return (rear  + 1) % maxSize == front;
	}
	
	// 判断队列是否为空
	public boolean isEmpty() {
		return rear == front;
	}
	
	// 添加数据到队列
	public void addQueue(int n) {
		// 判断队列是否满
		if (isFull()) {
			System.out.println("队列满，不能加入数据~");
			return;
		}
		//直接将数据加入
		arr[rear] = n;
		//将 rear 后移, 这里必须考虑取模
		rear = (rear + 1) % maxSize;
	}
	
	// 获取队列的数据, 出队列
	public int getQueue() {
		// 判断队列是否空
		if (isEmpty()) {
			// 通过抛出异常
			throw new RuntimeException("队列空，不能取数据");
		}
		// 这里需要分析出 front是指向队列的第一个元素
		// 1. 先把 front 对应的值保留到一个临时变量
		// 2. 将 front 后移, 考虑取模
		// 3. 将临时保存的变量返回
		int value = arr[front];
		front = (front + 1) % maxSize;
		return value;

	}
	
	// 显示队列的所有数据
	public void showQueue() {
		// 遍历
		if (isEmpty()) {
			System.out.println("队列空的，没有数据~~");
			return;
		}
		// 思路：从front开始遍历，遍历多少个元素
		// 动脑筋
		for (int i = front; i < front + size() ; i++) {
			System.out.printf("arr[%d]=%d\n", i % maxSize, arr[i % maxSize]);
		}
	}
	
	// 求出当前队列有效数据的个数
	public int size() {
		// rear = 2
		// front = 1
		// maxSize = 3 
		return (rear + maxSize - front) % maxSize;   
	}
	
	// 显示队列的头数据， 注意不是取出数据
	public int headQueue() {
		// 判断
		if (isEmpty()) {
			throw new RuntimeException("队列空的，没有数据~~");
		}
		return arr[front];
	}
}
```

# Link

## Single Link

```java
class SingleLinkedList {

	private final HeroNode head = new HeroNode(0, "", "");

	public HeroNode getHead() {
		return head;
	}

	public void add(HeroNode heroNode) {

		HeroNode temp = head;

		while (temp.next != null) {
			temp = temp.next;
		}
		temp.next = heroNode;
	}

	public void addByOrder(HeroNode heroNode) {

		HeroNode temp = head;
		boolean flag = false;
		while(true) {
			if(temp.next == null) {
				break;
			} 
			if(temp.next.no > heroNode.no) {
				break;
			} else if (temp.next.no == heroNode.no) {
				
				flag = true;
				break;
			}
			temp = temp.next;
		}

		if(flag) {
			System.out.printf("%d\n", heroNode.no);
		} else {

			heroNode.next = temp.next;
			temp.next = heroNode;
		}
	}

	public void update(HeroNode newHeroNode) {

		if(head.next == null) {
			System.out.println("链表为空");
			return;
		}

		HeroNode temp = head.next;
		boolean flag = false;
		while(true) {
			if (temp == null) {
				break;
			}
			if(temp.no == newHeroNode.no) {
				flag = true;
				break;
			}
			temp = temp.next;
		}

		if(flag) {
			temp.name = newHeroNode.name;
			temp.nickname = newHeroNode.nickname;
		} else {
			System.out.printf("%d\n", newHeroNode.no);
		}
	}
	
	public void del(int no) {
		HeroNode temp = head;
		boolean flag = false;
		while(true) {
			if(temp.next == null) {
				break;
			}
			if(temp.next.no == no) {
				flag = true;
				break;
			}
			temp = temp.next;
		}

		if(flag) {
			temp.next = temp.next.next;
		}else {
			System.out.printf("%d\n", no);
		}
	}
	

	public void list() {

		if(head.next == null) {
			System.out.println("???????");
			return;
		}

		HeroNode temp = head.next;
		while (temp != null) {

			System.out.println(temp);

			temp = temp.next;
		}
	}
}


class HeroNode {
	public int no;
	public String name;
	public String nickname;
	public HeroNode next;

	public HeroNode(int no, String name, String nickname) {
		this.no = no;
		this.name = name;
		this.nickname = nickname;
	}
	@Override
	public String toString() {
		return "HeroNode [no=" + no + ", name=" + name + ", nickname=" + nickname + "]";
	}
	
}
```

## Double Link

```java
// 创建一个双向链表的类
class DoubleLinkedList {

	// 先初始化一个头节点, 头节点不要动, 不存放具体的数据
	private final HeroNode2 head = new HeroNode2(0, "", "");

	// 返回头节点
	public HeroNode2 getHead() {
		return head;
	}

	// 遍历双向链表的方法
	// 显示链表[遍历]
	public void list() {
		// 判断链表是否为空
		if (head.next == null) {
			System.out.println("链表为空");
			return;
		}
		// 因为头节点，不能动，因此我们需要一个辅助变量来遍历
		HeroNode2 temp = head.next;
		while (temp != null) {
			// 判断是否到链表最后
			// 输出节点的信息
			System.out.println(temp);
			// 将temp后移， 一定小心
			temp = temp.next;
		}
	}

	// 添加一个节点到双向链表的最后.
	public void add(HeroNode2 heroNode) {

		// 因为head节点不能动，因此我们需要一个辅助遍历 temp
		HeroNode2 temp = head;
		// 遍历链表，找到最后
		//
		while (temp.next != null) {
			// 找到链表的最后
			// 如果没有找到最后, 将temp后移
			temp = temp.next;
		}
		// 当退出while循环时，temp就指向了链表的最后
		// 形成一个双向链表
		temp.next = heroNode;
		heroNode.pre = temp;
	}

	// 修改一个节点的内容, 可以看到双向链表的节点内容修改和单向链表一样
	// 只是 节点类型改成 HeroNode2
	public void update(HeroNode2 newHeroNode) {
		// 判断是否空
		if (head.next == null) {
			System.out.println("链表为空~");
			return;
		}
		// 找到需要修改的节点, 根据no编号
		// 定义一个辅助变量
		HeroNode2 temp = head.next;
		boolean flag = false; // 表示是否找到该节点
		while (true) {
			if (temp == null) {
				break; // 已经遍历完链表
			}
			if (temp.no == newHeroNode.no) {
				// 找到
				flag = true;
				break;
			}
			temp = temp.next;
		}
		// 根据flag 判断是否找到要修改的节点
		if (flag) {
			temp.name = newHeroNode.name;
			temp.nickname = newHeroNode.nickname;
		} else { // 没有找到
			System.out.printf("没有找到 编号 %d 的节点，不能修改\n", newHeroNode.no);
		}
	}

	// 从双向链表中删除一个节点,
	// 说明
	// 1 对于双向链表，我们可以直接找到要删除的这个节点
	// 2 找到后，自我删除即可
	public void del(int no) {

		// 判断当前链表是否为空
		if (head.next == null) {// 空链表
			System.out.println("链表为空，无法删除");
			return;
		}

		HeroNode2 temp = head.next; // 辅助变量(指针)
		boolean flag = false; // 标志是否找到待删除节点的
		while (true) {
			if (temp == null) { // 已经到链表的最后
				break;
			}
			if (temp.no == no) {
				// 找到的待删除节点的前一个节点temp
				flag = true;
				break;
			}
			temp = temp.next; // temp后移，遍历
		}
		// 判断flag
		if (flag) { // 找到
			// 可以删除
			// temp.next = temp.next.next;[单向链表]
			temp.pre.next = temp.next;
			// 这里我们的代码有问题?
			// 如果是最后一个节点，就不需要执行下面这句话，否则出现空指针
			if (temp.next != null) {
				temp.next.pre = temp.pre;
			}
		} else {
			System.out.printf("要删除的 %d 节点不存在\n", no);
		}
	}

}

// 定义HeroNode2 ， 每个HeroNode 对象就是一个节点
class HeroNode2 {
	public int no;
	public String name;
	public String nickname;
	public HeroNode2 next; // 指向下一个节点, 默认为null
	public HeroNode2 pre; // 指向前一个节点, 默认为null
	// 构造器

	public HeroNode2(int no, String name, String nickname) {
		this.no = no;
		this.name = name;
		this.nickname = nickname;
	}

	// 为了显示方法，我们重新toString
	@Override
	public String toString() {
		return "HeroNode [no=" + no + ", name=" + name + ", nickname=" + nickname + "]";
	}

}
```

# Stack

```java
public class LinkStack<T> {
    Node<T> top;
    int capacity=-1;
    //栈空
    public boolean isEmpty() {
        return top == null;
    }
    //入栈-push
    public void push(T value) {
        Node<T> node=new Node<T>();
        node.value=value;
        node.next=top;
        top=node;
        ++capacity;
    }
    //出栈-pop, 将栈顶的数据返回
    public T pop() {
        //先判断栈是否空
        if(isEmpty()) {
            //抛出异常
            throw new RuntimeException("栈空，没有数据~");
        }
        T value = top.value;
        top=top.next;
        --capacity;
        return value;
    }
    //显示栈的情况[遍历栈]， 遍历时，需要从栈顶开始显示数据
    public void list() {
        if(isEmpty()) {
            System.out.println("栈空，没有数据~~");
            return;
        }
        //需要从栈顶开始显示数据
        Node<T> current=top;
        for(int i = capacity; i >= 0 ; i--) {
            System.out.println("stack["+i+"]="+current.value);
            current=current.next;
        }
    }

}
class Node<T>{
    T value;
    Node<T> next;
}
```

# Hash Table

```java
//创建HashTab 管理多条链表
class HashTab {
	private final EmpLinkedList[] empLinkedListArray;
	private final int size; //表示有多少条链表
	
	//构造器
	public HashTab(int size) {
		this.size = size;
		//初始化empLinkedListArray
		empLinkedListArray = new EmpLinkedList[size];
		//？留一个坑, 这时不要分别初始化每个链表
		for(int i = 0; i < size; i++) {
			empLinkedListArray[i] = new EmpLinkedList();
		}
	}
	
	//添加雇员
	public void add(Emp emp) {
		//根据员工的id ,得到该员工应当添加到哪条链表
		int empLinkedListNO = hashFun(emp.id);
		//将emp 添加到对应的链表中
		empLinkedListArray[empLinkedListNO].add(emp);
		
	}
	//遍历所有的链表,遍历hashTab
	public void list() {
		for(int i = 0; i < size; i++) {
			empLinkedListArray[i].list(i);
		}
	}
	
	//根据输入的id,查找雇员
	public void findEmpById(int id) {
		//使用散列函数确定到哪条链表查找
		int empLinkedListNO = hashFun(id);
		Emp emp = empLinkedListArray[empLinkedListNO].findEmpById(id);
		if(emp != null) {//找到
			System.out.printf("在第%d条链表中找到 雇员 id = %d\n", (empLinkedListNO + 1), id);
		}else{
			System.out.println("在哈希表中，没有找到该雇员~");
		}
	}
	
	//编写散列函数, 使用一个简单取模法
	public int hashFun(int id) {
		return id % size;
	}
}
//表示一个雇员
class Emp {
	public int id;
	public String name;
	public Emp next; //next 默认为 null
	public Emp(int id, String name) {
		super();
		this.id = id;
		this.name = name;
	}
}
//创建EmpLinkedList ,表示链表
class EmpLinkedList {
	//头指针，执行第一个Emp,因此我们这个链表的head 是直接指向第一个Emp
	private Emp head; //默认null
	
	//添加雇员到链表
	//说明
	//1. 假定，当添加雇员时，id 是自增长，即id的分配总是从小到大
	//   因此我们将该雇员直接加入到本链表的最后即可
	public void add(Emp emp) {
		//如果是添加第一个雇员
		if(head == null) {
			head = emp;
			return;
		}
		//如果不是第一个雇员，则使用一个辅助的指针，帮助定位到最后
		Emp curEmp = head;
		//说明到链表最后
		while (curEmp.next != null) {
			curEmp = curEmp.next; //后移
		}
		//退出时直接将emp 加入链表
		curEmp.next = emp;
	}
	
	//遍历链表的雇员信息
	public void list(int no) {
		if(head == null) { //说明链表为空
			System.out.println("第 "+(no+1)+" 链表为空");
			return;
		}
		System.out.print("第 "+(no+1)+" 链表的信息为");
		Emp curEmp = head; //辅助指针
		while(true) {
			System.out.printf(" => id=%d name=%s\t", curEmp.id, curEmp.name);
			if(curEmp.next == null) {//说明curEmp已经是最后结点
				break;
			}
			curEmp = curEmp.next; //后移，遍历
		}
		System.out.println();
	}
	
	//根据id查找雇员
	//如果查找到，就返回Emp, 如果没有找到，就返回null
	public Emp findEmpById(int id) {
		//判断链表是否为空
		if(head == null) {
			System.out.println("链表为空");
			return null;
		}
		//辅助指针
		Emp curEmp = head;
		while(true) {
			if(curEmp.id == id) {//找到
				break;//这时curEmp就指向要查找的雇员
			}
			//退出
			if(curEmp.next == null) {//说明遍历当前链表没有找到该雇员
				curEmp = null;
				break;
			}
			curEmp = curEmp.next;//以后
		}
		
		return curEmp;
	}
}
```

# Tree

## AVL Tree

```java
// 创建AVLTree
class AVLTree {
	private Node root;

	public Node getRoot() {
		return root;
	}

	// 查找结点
	public Node search(int value) {
		if (root == null) {
			return null;
		} else {
			return root.search(value);
		}
	}
	//删除结点
    public void delNode(int value) {
        if (root != null){
            root=root.delete(value);
        }
    }


	// 添加结点的方法
	public void add(Node node) {
		if (root == null) {
			root = node;// 如果root为空则直接让root指向node
		} else {
			root.add(node);
		}
	}

	// 中序遍历
	public void infixOrder() {
		if (root != null) {
			root.infixOrder();
		} else {
			System.out.println("二叉排序树为空，不能遍历");
		}
	}
}

// 创建Node结点
class Node {
	int value;
	Node left;
	Node right;
	public Node(int value) {

		this.value = value;
	}

	// 返回左子树的高度
	public int leftHeight() {
		if (left == null) {
			return 0;
		}
		return left.height();
	}

	// 返回右子树的高度
	public int rightHeight() {
		if (right == null) {
			return 0;
		}
		return right.height();
	}

	// 返回 以该结点为根结点的树的高度
	public int height() {
		return Math.max(left == null ? 0 : left.height(), right == null ? 0 : right.height()) + 1;
	}
	
	//左旋转方法
	private void leftRotate() {
		//创建新的结点，以当前根结点的值
		Node newNode = new Node(value);
		//把新的结点的左子树设置成当前结点的左子树
		newNode.left = left;
		//把新的结点的右子树设置成右子树的左子树
		newNode.right = right.left;

		//把当前结点的值替换成右子结点的值
		value = right.value;
		//把当前结点的右子树设置成当前结点右子树的右子树
		right = right.right;

		//把当前结点的左子树(左子结点)设置成新的结点
		left = newNode;
	}
	
	//右旋转
	private void rightRotate() {
		Node newNode = new Node(value);

		newNode.right = right;

		newNode.left = left.right;

		value = left.value;

		left = left.left;

		right = newNode;
	}

	// 查找要删除的结点
	/**
	 * 
	 * @param value
	 *            希望删除的结点的值
	 * @return 如果找到返回该结点，否则返回null
	 */
	public Node search(int value) {
		if (value == this.value) { // 找到就是该结点
			return this;
		} else if (value < this.value) {// 如果查找的值小于当前结点，向左子树递归查找
			// 如果左子结点为空
			if (this.left == null) {
				return null;
			}
			return this.left.search(value);
		} else { // 如果查找的值不小于当前结点，向右子树递归查找
			if (this.right == null) {
				return null;
			}
			return this.right.search(value);
		}

	}


	@Override
	public String toString() {
		return "Node [value=" + value + "]";
	}

	// 添加结点的方法
	// 递归的形式添加结点，注意需要满足二叉排序树的要求
	public void add(Node node) {
		if (node == null) {
			return;
		}

		// 判断传入的结点的值，和当前子树的根结点的值关系
		if (node.value < value) {
			// 如果当前结点左子结点为null
			if (left == null) {
				left = node;
			} else {
				// 递归的向左子树添加
				left.add(node);
			}
		} else { // 添加的结点的值大于 当前结点的值
			if (right == null) {
				right = node;
			} else {
				// 递归的向右子树添加
				right.add(node);
			}

		}
		rotate();
	}

	// 中序遍历
	public void infixOrder() {
		if (this.left != null) {
			this.left.infixOrder();
		}
		System.out.println(this);
		if (this.right != null) {
			this.right.infixOrder();
		}
	}



	public void rotate(){
		//当添加完一个结点后，如果: (右子树的高度-左子树的高度) > 1 , 左旋转
		if(rightHeight() - leftHeight() > 1) {
			//如果它的右子树的左子树的高度大于它的右子树的右子树的高度
			if(right != null && right.leftHeight() > right.rightHeight()) {
				//先对右子结点进行右旋转
				right.rightRotate();
				//然后在对当前结点进行左旋转
			}
			//直接进行左旋转即可
			leftRotate(); //左旋转..
			return ; //必须要!!!
		}

		//当添加完一个结点后，如果 (左子树的高度 - 右子树的高度) > 1, 右旋转
		if(leftHeight() - rightHeight() > 1) {
			//如果它的左子树的右子树高度大于它的左子树的高度
			if(left != null && left.rightHeight() > left.leftHeight()) {
				//先对当前结点的左结点(左子树)->左旋转
				left.leftRotate();
			}
			//再对当前结点进行右旋转
			rightRotate();
		}
	}


    //删除
    public Node delete(int value) {
        Node node=this;
        if (this.value==value){
            if (left!=null&&right!=null){
                Node min=right;
                while (min.left!=null) min = min.left;
                value=min.value;
                this.value=value;
                right=right.delete(value);
            }else node=(left==null)?right:left;
        }else if (right!=null&&this.value<value){
            right=right.delete(value);
        }
        else if (left!=null&&this.value>value) {
            left=left.delete(value);
        }
        else return null;
        if (node!=null) node.rotate();
        return node;
    }
}
```

## Array Binary Tree

设父节点索引为$n$，则左子节点索引为$2n+1$，右子节点索引为$2n+2$。

### Thread

```java
//中序索引，将空的左右子节点利用起来
public void threadedNodes(HeroNode node) {
	if(node == null) return;
	threadedNodes(node.getLeft());
	if(node.getLeft() == null) {
		node.setLeft(pre);
		node.setLeftType(1);
	}
	if (pre != null && pre.getRight() == null) {
		pre.setRight(node);
		pre.setRightType(1);
	}
	pre = node;
	threadedNodes(node.getRight());
}

public void threadedList() {
	HeroNode node = root;
	while(node != null) {
		while(node.getLeftType() == 0) node = node.getLeft();
		System.out.println(node);
		while(node.getRightType() == 1) {
			node = node.getRight();
			System.out.println(node);
		}
		node = node.getRight();
	}
}
```

## Binary Sort Tree

```java
//创建二叉排序树
class BinarySortTree {
	private Node root;

	public Node getRoot() {
		return root;
	}

	//查找要删除的结点
	public Node search(int value) {
		if(root == null) return null;
		else return root.search(value);
	}

	//删除结点
	public void delNode(int value) {
		if (root != null){
			root=root.delete(value);
		}
	}
	
	//添加结点的方法
	public void add(Node node) {
		if (node != null) {
			if (root == null) root = node;//如果root为空则直接让root指向node
			else root.add(node);
		}
	}
	//中序遍历
	public void infixOrder() {
		if(root != null) root.infixOrder();
		else System.out.println("二叉排序树为空，不能遍历");
	}
}

//创建Node结点
class Node {
	int value;
	Node left;
	Node right;

	@Override
	public String toString() {
		return "Node{" +
				"value=" + value +
				'}';
	}

	public Node(int value) {
		this.value = value;
	}
	//查找要删除的结点
	/**
	 *
	 * @param value 希望删除的结点的值
	 * @return 如果找到返回该结点，否则返回null
	 */
	public Node search(int value) {
		//找到就是该结点
		if(value == this.value) return this;
		else if(value < this.value) {//如果查找的值小于当前结点，向左子树递归查找
			//如果左子结点为空
			if(this.left  == null) return null;
			return this.left.search(value);
		} else { //如果查找的值不小于当前结点，向右子树递归查找
			if(this.right == null) return null;
			return this.right.search(value);
		}
	}

	//添加结点的方法
	//递归的形式添加结点，注意需要满足二叉排序树的要求
	public void add(Node node) {
		if (node==null) return;
		//判断传入的结点的值，和当前子树的根结点的值关系
		//添加的结点的值大于或等于当前结点的值
		if(node.value < value) {
			if(left == null) {
				left = node;//如果当前结点左子结点为null
			}
			else left.add(node);//递归的向左子树添加
		} else
			if (right == null) {
				right = node;
			}
			else right.add(node);//递归的向右子树添加
	}
	//中序遍历
	public void infixOrder() {
		if(this.left != null) this.left.infixOrder();
		System.out.println(this);
		if(this.right != null) this.right.infixOrder();
	}

	//删除
	public Node delete(int value) {
		Node node=this;
		if (this.value==value){
			if (left!=null&&right!=null){
				Node min=right;
				while (min.left!=null) min = min.left;
				value=min.value;
				this.value=value;
				right=right.delete(value);
			}else node=(left==null)?right:left;
		}else if (right!=null&&this.value<value) right=right.delete(value);
		else if (left!=null&&this.value>value) left=left.delete(value);
		else return null;
		return node;
	}
}
```

# graph