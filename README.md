# DSA-3A16
DSA programme class work  

--------------------------------------------------------------------------------------------* 22-09-2023 *--------------------------------------------------------------------------------------------------------------------
 (https://drive.google.com/drive/folders/1456KER2zpwMhGbEa7EdU9euIch2nkbYF)
 ---LAB WORK EXAMPLE 8---
 --CODE--
 
 #include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* left;
    struct Node* right;
};
struct Node* newNode(int data) {
    struct Node* node = (struct Node*)malloc(sizeof(struct Node));
    node->data = data;
    node->left = NULL;
    node->right = NULL;
    return node;
}
int height(struct Node* root) {
    if (root == NULL) {
        return -1;
    } else {
        int leftHeight = height(root->left);
        int rightHeight = height(root->right);
        return (leftHeight > rightHeight) ? (leftHeight + 1) : (rightHeight + 1);
    }
}

int main() {
    struct Node* root = newNode(1);
    root->left = newNode(8);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->left->left->left = newNode(5);
    root->left->left->right = newNode(10);
    root->left->left->left->left= newNode(5);
    printf("Height of the binary tree is: %d\n", height(root));

    return 0;
}
--OUTPUT--
Height of the binary tree is: 4
