import java.util.Scanner;

class Node {
    String task;
    Node next;

    public Node(String task) {
        this.task = task;
        this.next = null;
    }
}

public class ListLinkList {
    Node head;

    public ListLinkList() {
        head = null;
    }

    // Adds a new task to the end of the linked list
    public void addTask(String task) {
        Node newNode = new Node(task);
        if (head == null) { // if the list is empty, the new node becomes the head
            head = newNode;
        } else {
            Node current = head;
            // Iterate through the list until the last node
            while (current.next != null) {
                current = current.next;
            }
            // Attach the new node to the end of the list
            current.next = newNode;
        }
        System.out.println("Task " + task + " added to the list.");
    }

    // Deletes a task from the linked list
    public void deleteTask(String task) {
        if (head == null) { // If the list is empty, there's nothing to delete
            System.out.println("The list is empty.");
            return;
        }
        if (head.task.equals(task)) { // If the task is the first one in the list
            head = head.next;
            System.out.println("Task " + task + " deleted from the list.");
            return;
        }

        Node current = head;
        // Iterate through the list to find the task
        while (current.next != null) {
            if (current.next.task.equals(task)) {
                // Remove the task by linking the previous node to the node after the one to be deleted
                current.next = current.next.next;
                System.out.println("Task " + task + " deleted from the list.");
                return;
            }
            current = current.next;
        }
        System.out.println("Task " + task + " not found in the list.");
    }

    // Displays all the tasks in the linked list
    public void viewTasks() {
        if (head == null) { // If the list is empty, there's nothing to display
            System.out.println("The list is empty.");
            return;
        }
        System.out.println("To-Do List:");
        Node current = head;
        // Iterate through the list and print each task
        while (current != null) {
            System.out.println("- " + current.task);
            current = current.next;
        }
    }

    public static void main(String[] args) {
        ListLinkList list = new ListLinkList();
        Scanner scanner = new Scanner(System.in);

        while (true) {
            System.out.println("\n---To-Do List---");
            System.out.println("1. Add task");
            System.out.println("2. Delete task");
            System.out.println("3. View All Tasks");
            System.out.println("4. Exit");
            System.out.print("Enter your choice: ");
            int choice = scanner.nextInt();
            scanner.nextLine(); // consume newline character

            switch (choice) {
                case 1:
                    System.out.print("Enter task description: ");
                    String task = scanner.nextLine();
                    list.addTask(task);
                    break;
                case 2:
                    System.out.print("Enter task to delete: ");
                    String taskToDelete = scanner.nextLine();
                    list.deleteTask(taskToDelete);
                    break;
                case 3:
                    list.viewTasks();
                    break;
                case 4:
                    System.out.println("Exiting...");
                    scanner.close();
                    return;
                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        }
    }
}
