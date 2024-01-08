# to-do-list
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
typedef struct TaskNode {
 char task[100];
 struct TaskNode* next;
} TaskNode;
TaskNode* createTaskNode(const char* task) {
 TaskNode* newNode = (TaskNode*)malloc(sizeof(TaskNode));
 if (newNode == NULL) {
 printf("Memory allocation failed.\n");
 exit(EXIT_FAILURE);
 }
 strcpy(newNode->task, task);
 newNode->next = NULL;
 return newNode;
}
void addTask(TaskNode** head, const char* task) {
 TaskNode* newNode = createTaskNode(task);
 newNode->next = *head;
 *head = newNode;
1
0
 printf("Task added: %s\n", task);
}
void removeTask(TaskNode** head, const char* task) {
 TaskNode* current = *head;
 TaskNode* prev = NULL;
 while (current != NULL && strcmp(current->task, task) != 0) {
 prev = current;
 current = current->next;
 }
 if (current == NULL) {
 printf("Task not found: %s\n", task);
 return;
 }
 if (prev == NULL) {
 *head = current->next;
 } else {
 prev->next = current->next;
 }
 free(current);
 printf("Task removed: %s\n", task);
}
1
1
void displayTasks(TaskNode* head) {
 if (head == NULL) {
 printf("Task list is empty.\n");
 return;
 }
 printf("Current Tasks:\n");
 while (head != NULL) {
 printf("- %s\n", head->task);
 head = head->next;
 }
}
void freeTasks(TaskNode* head) {
 while (head != NULL) {
 TaskNode* temp = head;
 head = head->next;
 free(temp);
 }
}
int main() {
 TaskNode* taskList = NULL;
 char userInput[100];
 while (1) {
1
2
 printf("\nEnter 'add' to add a task \n'remove' to remove a task \n'display' to show tasks '\nexit' to exit:\n ");
 fgets(userInput, sizeof(userInput), stdin);
 userInput[strcspn(userInput, "\n")] = '\0'; // Remove trailing newline
 if (strcmp(userInput, "add") == 0) {
 printf("Enter task to add: ");
 fgets(userInput, sizeof(userInput), stdin);
 userInput[strcspn(userInput, "\n")] = '\0'; // Remove trailing newline
 addTask(&taskList, userInput);
 } else if (strcmp(userInput, "remove") == 0) {
 printf("Enter task to remove: ");
 fgets(userInput, sizeof(userInput), stdin);
 userInput[strcspn(userInput, "\n")] = '\0'; // Remove trailing newline
 removeTask(&taskList, userInput);
 } else if (strcmp(userInput, "display") == 0) {
 displayTasks(taskList);
 } else if (strcmp(userInput, "exit") == 0) {
 break;
 } else {
 printf("Invalid command. Please try again.\n");
 }
 } freeTasks(taskList); return 0;}
1
3
 
