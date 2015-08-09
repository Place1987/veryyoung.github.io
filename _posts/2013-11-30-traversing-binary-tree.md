---
layout: post
title: 二叉树遍历
date: 2013-11-30 02:30
author: VERYYOUNG
comments: true
categories: [Algorithm]
---
赶到该公司第一件事就是做一套笔试题，笔试题有三题，这里说说第一题
第一题是二叉树非递归层次遍历
用队列实现，代码如下:
<pre lang="java">
    static void levelorder(Node p) {
        if (p == null) return;
        Queue<Node> queue = new LinkedList<Node>();
        queue.offer(p);
        while (queue.size() > 0) {
            Node temp = queue.poll();
            visit(temp);
            if (temp.getLeft() != null) {
                queue.offer(temp.getLeft());
            }
            if (temp.getRight() != null) {
                queue.offer(temp.getRight());
            }
        }
    }
</pre>

顺便给出前中后序的递归遍历：
前序：
<pre lang="java">
    static void preorder(Node p) {
        if (p != null) {
            visit(p);
            preorder(p.getLeft());
            preorder(p.getRight());
        }
    }
</pre>

中序：
<pre lang="java">
    static void inorder(Node p) {
        if (p != null) {
            inorder(p.getLeft());
            visit(p);
            inorder(p.getRight());
        }
    }
</pre>

后序：
<pre lang="java">
    static void preorder(Node p) {
    static void postorder(Node p) {
        if (p != null) {
            postorder(p.getLeft());
            postorder(p.getRight());
            visit(p);
        }
    }
</pre>

这三种就是访问根的顺序不同。
(1)先序遍历 
访问根；按先序遍历左子树；按先序遍历右子树 
(2)中序遍历 
按中序遍历左子树；访问根；按中序遍历右子树 
(3)后序遍历 
按后序遍历左子树；按后序遍历右子树；访问根 
（4）层次遍历 
即按照层次访问，通常用队列来做。访问根，访问子女，再访问子女的子女（越往后的层次越低）（两个子女的级别相同） 

贴上有关二叉树的一些操作的代码：
<pre lang="java">

/**
 * Created with IntelliJ IDEA.
 * User: veryyoung
 * Email:codingyoung@gmail.com
 * Date: 13-11-30
 * Time: 上午2:02
 * To change this template use File | Settings | File Templates.
 */

import java.util.ArrayList;
import java.util.LinkedList;
import java.util.List;
import java.util.Queue;

public class BinaryTree {
    protected Node root;

    public BinaryTree(Node root) {
        this.root = root;
    }

    /**
     * 构造树
     */
    public static Node init() {
        Node a = new Node('A');
        Node b = new Node('B', null, a);
        Node c = new Node('C');
        Node d = new Node('D', b, c);
        Node e = new Node('E');
        Node f = new Node('F', e, null);
        Node g = new Node('G', null, f);
        Node h = new Node('H', d, g);
        return h;// root
    }

    /**
     * 访问节点
     */
    public static void visit(Node p) {
        System.out.print(p.getKey() + " ");
    }

    /**
     * 递归实现前序遍历
     */
    static void preorder(Node p) {
        if (p != null) {
            visit(p);
            preorder(p.getLeft());
            preorder(p.getRight());
        }
    }

    /**
     * 递归实现中序遍历
     */
    static void inorder(Node p) {
        if (p != null) {
            inorder(p.getLeft());
            visit(p);
            inorder(p.getRight());
        }
    }

    /**
     * 递归实现后序遍历
     */
    static void postorder(Node p) {
        if (p != null) {
            postorder(p.getLeft());
            postorder(p.getRight());
            visit(p);
        }
    }

    /**
     * 层次遍历
     */
    static void levelorder(Node p) {
        if (p == null) return;
        Queue<Node> queue = new LinkedList<Node>();
        queue.offer(p);
        while (queue.size() > 0) {
            Node temp = queue.poll();
            visit(temp);
            if (temp.getLeft() != null) {
                queue.offer(temp.getLeft());
            }
            if (temp.getRight() != null) {
                queue.offer(temp.getRight());
            }
        }
    }

    // 求二叉树的高度
    static int height(Node tree) {
        if (tree == null)
            return 0;
        else {
            int leftTreeHeight = height(tree.getLeft());
            int rightTreeHeight = height(tree.getRight());
            ;
            return leftTreeHeight > rightTreeHeight ? leftTreeHeight + 1 : rightTreeHeight + 1;
        }
    }

    // 求二叉树的结点总数
    static int nodes(Node tree) {
        if (tree == null)
            return 0;
        else {
            int left = nodes(tree.getLeft());
            int right = nodes(tree.getRight());
            return left + right + 1;
        }
    }

    // 求二叉树叶子节点的总数
    static int leaf(Node tree) {
        if (tree == null)
            return 0;
        else {
            int left = leaf(tree.getLeft());
            int right = leaf(tree.getRight());
            if (tree.getLeft() == null && tree.getRight() == null)
                return left + right + 1;
            else
                return left + right;
        }
    }

    //将二叉树所有结点的左右子树交换
    static void swapTree(Node root) {
        if (root != null) {
            Node tmp = root.getLeft();
            root.setLeft(root.getRight());
            root.setRight(tmp);
            swapTree(root.getLeft());
            swapTree(root.getRight());
        }
    }

    /**
     * getLeafNodes: 递归求解给定二叉树的所有叶子结点
     *
     * @param root     给定二叉树的根结点
     * @param leaflist 给定二叉树的所有叶子结点
     */
    static void getLeafNodes(Node root, List<Node> leaflist) {
        if (root != null) {
            if (root.getLeft() == null && root.getRight() == null) {
                leaflist.add(root);
                return;
            }
            getLeafNodes(root.getLeft(), leaflist);
            getLeafNodes(root.getRight(), leaflist);
        }
    }

    /**
     * longestPath: 递归求解给定二叉树的一条最长路径 如果有多条，输出其中一条
     *
     * @param root        给定二叉树的根结点
     * @param longestPath 存放二叉树的最长路径上的结点
     */
    static void longestPath(Node root, List<Node> longestPath) {
        if (root != null) {
            longestPath.add(root);
            if (root.getLeft() == null && root.getRight() == null) { // 左右子树均空
                return;
            }

            List<Node> leftLongestPath = new ArrayList<Node>();
            List<Node> rightLongestPath = new ArrayList<Node>();
            longestPath(root.getLeft(), leftLongestPath);
            longestPath(root.getRight(), rightLongestPath);
            if (leftLongestPath.size() >= rightLongestPath.size()) {
                longestPath.addAll(leftLongestPath);
            } else if (leftLongestPath.size() < rightLongestPath.size()) {
                longestPath.addAll(rightLongestPath);

            }
        }
    }

    /**
     * @param args
     */
    public static void main(String[] args) {
        BinaryTree tree = new BinaryTree(init());
        System.out.print(" 前序遍历:");
        preorder(tree.getRoot());
        System.out.println();
        System.out.print(" 中序遍历:");
        inorder(tree.getRoot());
        System.out.println();
        System.out.print(" 后序遍历:");
        postorder(tree.getRoot());
        System.out.println();
        System.out.println();

        System.out.println("层次遍历");
        levelorder(tree.getRoot());
        System.out.println();
        System.out.println();
        System.out.println("叶子结点数");
        System.out.println(leaf(tree.getRoot()));
        System.out.println("总结点数");
        System.out.println(nodes(tree.getRoot()));
        System.out.println("树的高度");
        System.out.println(height(tree.getRoot()));

    }

    public Node getRoot() {
        return root;
    }

}

class Node {
    private char key;
    private Node left, right;

    public Node(char key) {
        this(key, null, null);
    }

    public Node(char key, Node left, Node right) {
        this.key = key;
        this.left = left;
        this.right = right;
    }

    public char getKey() {
        return key;
    }

    public void setKey(char key) {
        this.key = key;
    }

    public Node getLeft() {
        return left;
    }

    public void setLeft(Node left) {
        this.left = left;
    }

    public Node getRight() {
        return right;
    }

    public void setRight(Node right) {
        this.right = right;
    }
}
</pre>
