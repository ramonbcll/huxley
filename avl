#include <stdio.h>
#include <stdlib.h>

typedef struct bt bt;

struct bt {
  int item;
  int h;
	bt *left;
	bt *right;
};

bt* create_bt(int item, bt *left, bt *right) {
	bt *new_bt = (bt*) malloc(sizeof(bt));
	new_bt->item = item;
	new_bt->left = left;
	new_bt->right = right;
	
	return new_bt;
}

void print(bt *bt) {
  if(bt == NULL) {
   	printf(" () ");
   	return;
  }
  else {
   	printf("( %d ", bt->item);
   	print(bt->left);
   	print(bt->right);
   	printf(") ");
  }
}

int max(int a, int b) {
  return (a > b) ? a : b;
}

int h(bt* tree) {
  if(tree == NULL) {
    return -1;
  }
  else {
    return 1 + max(h(tree->left), h(tree->right));
  }
}

int isBalanced(bt* tree) {
  int bf = h(tree->left) - h(tree->right);
  return ((-1 <= bf) && (bf <= 1));
}

bt* rotate_left(bt *tree) {
  bt *subtree_root = NULL;
  if (tree != NULL && tree->right != NULL) {
    subtree_root = tree->right;
    tree->right = subtree_root->left;
    subtree_root->left = tree;
  }
  subtree_root->h = h(subtree_root);
  tree->h = h(tree);
  return subtree_root;
}

bt* rotate_right(bt *tree) {
  bt *subtree_root = NULL;
  if (tree != NULL && tree->left != NULL) {
    subtree_root = tree->left;
    tree->left = subtree_root->right;
    subtree_root->right = tree;
  }
  subtree_root->h = h(subtree_root);
  tree->h = h(tree);
  return subtree_root;
}

int balance_factor(bt *bt) {
  if (bt == NULL) {
    return 0;
  } 
  else if ((bt->left != NULL) && (bt->right != NULL)) {
    return (bt->left->h - bt->right->h);
  }  
  else if ((bt->left != NULL) && (bt->right == NULL)) {
    return (1 + bt->left->h);
  }
  else {
    return (-bt->right->h - 1);
  }
}

bt* add(bt *tree, int item) {
  if (tree == NULL) {
    return create_bt(item, NULL, NULL);
  }
  else if (tree->item > item) {
    tree->left = add(tree->left, item);
  } 
  else {
    tree->right = add(tree->right, item);
  }
  tree->h = h(tree);
  bt *child;
  if (balance_factor(tree) == 2 || balance_factor(tree) == -2) {
    if (balance_factor(tree) == 2) {
      child = tree->left;
      if (balance_factor(child) == -1) {
        tree->left = rotate_left(child);
      }
      tree = rotate_right(tree);
    }  
    else if (balance_factor(tree) == -2) {
      child = tree->right;
      if (balance_factor(child) == 1) {
        tree->right = rotate_right(child);
      }
      tree = rotate_left(tree);
    }
  }
  return tree;
}

int main() {
  int n;
  bt* bt = NULL;
  while (scanf("%d", &n) != EOF) {
   	bt = add(bt, n);
   	// printf("----\nAdicionando %d\n", n);
   	// printf("  ");
   	// print(bt);
   	// printf("\n");
  }
  print(bt);
  printf("\n----\n");

	return 0;
}
