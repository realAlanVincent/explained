This C program implements a Doubly Linked List (DLL) with various insertion and deletion operations. A doubly linked list consists of nodes, where each node contains three parts:

1. Data (integer value in this case).


2. Pointer to the previous node (prev).


3. Pointer to the next node (next).



Each operation in this program modifies the list structure dynamically.


---

Understanding the Code Step by Step

1. Structure Definition (struct Node)

typedef struct Node
{
    int data;
    struct Node *prev;
    struct Node *next;
} Node;

This defines a Node structure with three fields:

data: Holds the integer value.

prev: Points to the previous node.

next: Points to the next node.



2. Global Head Pointer

Node *head = NULL;

head is a pointer that always points to the first node of the list.

Initially, the list is empty, so head is set to NULL.



---

Insertion Operations

3. Insert at Beginning (insertAtBeginning)

void insertAtBeginning(int value)
{
    Node *newNode = (Node *)malloc(sizeof(Node)); // Allocate memory
    newNode->data = value;
    newNode->prev = NULL; // Since it will be the first node
    newNode->next = head; // Link it to the current first node

    if (head != NULL)
    {
        head->prev = newNode; // Update old head's previous pointer
    }

    head = newNode; // Update head to the new node
}

How It Works

1. A new node is created dynamically using malloc.


2. It is assigned the given value.


3. The prev pointer is set to NULL (because it will be the first node).


4. The next pointer is set to the current head (to link with the existing list).


5. If the list is not empty, update the previous head node’s prev pointer to point to the new node.


6. Update head to point to the new node.



4. Insert at End (insertAtEnd)

void insertAtEnd(int value)
{
    Node *newNode = (Node *)malloc(sizeof(Node));
    newNode->data = value;
    newNode->next = NULL;

    if (head == NULL) // If list is empty
    {
        newNode->prev = NULL;
        head = newNode;
        return;
    }

    Node *temp = head;
    while (temp->next != NULL) // Traverse to the last node
    {
        temp = temp->next;
    }

    temp->next = newNode;
    newNode->prev = temp; // Link new node to the last node
}

How It Works

1. A new node is created.


2. If the list is empty, the new node becomes the head.


3. Otherwise, traverse to the last node.


4. Insert the new node at the end by adjusting next and prev pointers.



5. Insert at a Specific Position (insertAtPosition)

void insertAtPosition(int value, int position)
{
    Node *newNode = (Node *)malloc(sizeof(Node));
    newNode->data = value;

    if (position == 1) // Special case: insert at beginning
    {
        newNode->next = head;
        newNode->prev = NULL;
        if (head != NULL)
        {
            head->prev = newNode;
        }
        head = newNode;
        return;
    }

    Node *temp = head;
    for (int i = 1; temp != NULL && i < position - 1; i++) // Move to position
    {
        temp = temp->next;
    }

    if (temp == NULL) // Invalid position
    {
        printf("Invalid position\n");
        free(newNode);
        return;
    }

    newNode->next = temp->next;
    newNode->prev = temp;
    if (temp->next != NULL) // If not inserting at last position
    {
        temp->next->prev = newNode;
    }
    temp->next = newNode;
}

How It Works

1. If position is 1, call insertAtBeginning().


2. Otherwise, traverse to the position - 1 node.


3. If position is valid, insert the new node between temp and temp->next.


4. Adjust prev and next pointers.




---

Deletion Operations

6. Delete at Beginning (deleteAtBeginning)

void deleteAtBeginning()
{
    if (head == NULL)
    {
        printf("List is empty\n");
        return;
    }

    Node *temp = head;
    head = head->next; // Move head to the second node

    if (head != NULL)
    {
        head->prev = NULL; // Remove previous pointer of new head
    }

    free(temp);
}

How It Works

1. If the list is empty, print an error message.


2. Move head to the second node.


3. If the new head exists, set its prev pointer to NULL.


4. Free the old head.



7. Delete at End (deleteAtEnd)

void deleteAtEnd()
{
    if (head == NULL)
    {
        printf("List is empty\n");
        return;
    }

    Node *temp = head;
    while (temp->next != NULL)
    {
        temp = temp->next;
    }

    if (temp->prev != NULL) // If more than one node exists
    {
        temp->prev->next = NULL;
    }
    else // If only one node exists
    {
        head = NULL;
    }

    free(temp);
}

How It Works

1. If the list is empty, print an error.


2. Traverse to the last node.


3. If there's only one node, set head = NULL.


4. Otherwise, update the second last node’s next pointer to NULL.


5. Free the last node.



8. Delete at a Specific Position (deleteAtPosition)

void deleteAtPosition(int position)
{
    if (head == NULL)
    {
        printf("List is empty\n");
        return;
    }

    Node *temp = head;
    if (position == 1) // Special case: delete first node
    {
        head = head->next;
        if (head != NULL)
        {
            head->prev = NULL;
        }
        free(temp);
        return;
    }

    for (int i = 1; temp != NULL && i < position; i++)
    {
        temp = temp->next;
    }

    if (temp == NULL)
    {
        printf("Invalid position\n");
        return;
    }

    if (temp->next != NULL)
    {
        temp->next->prev = temp->prev;
    }

    if (temp->prev != NULL)
    {
        temp->prev->next = temp->next;
    }

    free(temp);
}

How It Works

1. If the list is empty, print an error.


2. If position is 1, update head and free the first node.


3. Otherwise, traverse to the target node.


4. Adjust prev and next pointers to remove it.


5. Free the node.




---

9. Printing the List (printList)

void printList()
{
    Node *temp = head;
    while (temp != NULL)
    {
        printf("%d", temp->data);
        if (temp->next != NULL)
        {
            printf(" <-> ");
        }
        temp = temp->next;
    }
    printf("\n");
}

Traverses the list and prints each node’s data.



---

10. Menu-Driven main() Function

Uses a while (1) loop to repeatedly ask for user input.

Calls the appropriate function based on user choice.



---

Summary

Implements a doubly linked list with insertion, deletion, and traversal.

Uses dynamic memory allocation (malloc and free).

Uses menu-driven input handling.


Would you like any modifications or explanations on specific parts?

