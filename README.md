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
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
2))
---LAB WORK EXAMPLE 9---
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
struct Node* insert(struct Node* root, int data) {
    if (root == NULL) {
        return newNode(data);
    }

    if (data < root->data) {
        root->left = insert(root->left, data);
    } else if (data > root->data) {
        root->right = insert(root->right, data);
    }

    return root;
}
struct Node* minValueNode(struct Node* node) {
    struct Node* current = node;
    while (current && current->left != NULL) {
        current = current->left;
    }
    return current;
}
struct Node* deleteNode(struct Node* root, int data) {
    if (root == NULL) {
        return root;
    }

    if (data < root->data) {
        root->left = deleteNode(root->left, data);
    } else if (data > root->data) {
        root->right = deleteNode(root->right, data);
    } else {
        if (root->left == NULL) {
            struct Node* temp = root->right;
            free(root);
            return temp;
        } else if (root->right == NULL) {
            struct Node* temp = root->left;
            free(root);
            return temp;
        }

        struct Node* temp = minValueNode(root->right);
        root->data = temp->data;
        root->right = deleteNode(root->right, temp->data);
    }
    return root;
}

void inorder(struct Node* root) {
    if (root != NULL) {
        inorder(root->left);
        printf("%d ", root->data);
        inorder(root->right);
    }
}

int main() {
    struct Node* root = NULL;
    root = insert(root, 50);
    root = insert(root, 30);
    root = insert(root, 20);
    root = insert(root, 40);
    root = insert(root, 70);
    root = insert(root, 60);
    root = insert(root, 80);

    printf("Inorder traversal before deletion: ");
    inorder(root);
    printf("\n");

    int key = 50;
    root = deleteNode(root, key);

    printf("Inorder traversal after deleting %d: ", key);
    inorder(root);
    printf("\n");

    return 0;
}
--OUTPUT--
Inorder traversal before deletion: 20 30 40 50 60 70 80 
Inorder traversal after deleting 50: 20 30 40 60 70 80 
